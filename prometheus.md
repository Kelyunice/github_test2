# Installation of prometheus:
```
wget https://github.com/prometheus/prometheus/releases/download/v2.26.0/prometheus-2.26.0.linux-amd64.tar.gz
```
2. Extract the archive:

```
 tar xvfz tar xvfz prometheus-2.26.0.linux-amd64.tar.gz
```

```
cd prometheus-2.26.0.linux-amd64
```

3. configure peometheus:

  vi in to the prometheus configuration file file

  vi prometheus.yaml
     - in global config :adjust the scrape interval
     - scrape_config: adjust the job name and the target

4. Start prometheus

```
  ./prometheus &
```
  access prometheus on the browser



 localhost:9090 or machine-ip:9090 

 work with the expression browser
```
 prometheus_tsdb_head_samples_appended_total
```
```
 rate(prometheus_tsdb_head_samples_appended_total[1m]
```

```
 up{job="prometheus"}
```

 ## Using the expression browser of prometheus

1. we can see the total number of samples ingested into Prometheus's local storage since process start time
   ```
   prometheus_tsdb_head_samples_appended_total
   ```

2. we can see the number of samples ingested per second as averaged over a 1-minute window
  
```
 rate(prometheus_tsdb_head_samples_appended_total[1])
```
3. we can see the value of the synthetic up metric for the Prometheus target, which is set to 0 when a scrape fails and 
   to 1 when it succeeds

   up{job="prometheus"}


## Querying the TSDB of prometheus using a Demo service of three instances ==============


1. Downloand the file:

```
wget https://github.com/juliusv/prometheus_demo_service/releases/download/0.0.4/prometheus_demo_service-0.0.4.linux.amd64.tar.gz
```

2. extract the archive:
```
tar xvfz prometheus_demo_service-0.0.4.linux.amd64.tar.gz
```

3. Run the demo service:
```
./prometheus_demo_service -listen-address=:10000 &

./prometheus_demo_service -listen-address=:10001 &

./prometheus_demo_service -listen-address=:10002 &
```

4. We need to adjust the scrape_configs section of the prometheus.yml so prometheus can scrape the service instances
```
  - job_name:'demo'
    static_configs:
      - targets:
        - 'localhost:10000'
        - 'localhost:10001'
        - 'localhost:10002
```
5. Reload the prometheus configuration file

```
  killall -HUP prometheus
```
6. Selecting Series:
   
   Before you can do anything more useful in PromQL,you have to learn how to select series data from the TSDB.

   The simplest way to do so is to ask for all series that have a certain metric name. 
   The query for this is simply the metric name itself.
```
demo_api_request_duration_seconds_count
```

```
   demo_api_request_duration_seconds_count{status="200"}
```
   You can also filter by multiple label conditions like this:

```
   demo_api_request_duration_seconds_count{method="GET",status="200"}
```

```
 demo_api_request_duration_seconds_count{job="demo"}
```

7. Computing Rate of Increase: counter metrics work for the following functions:

   i. rate()
   ii. irate()
   iii. increase() 

```
   rate(demo_api_request_duration_seconds_count{job="demo"}[5m])

   irate(demo_api_request_duration_seconds_count{job="demo"}[5m])
```
8. Computing Derivatives: this is done for guage metrics that can go up or down(like temperation, memory usage or free disk space)
  use the following functions:
   i. delta()
   ii. deriv()

   iii. predict_linear()

   the predict linear function will help to predict what a guage will be in a given amount of time in the future
```
   delta(demo_disk_usage_bytes{job="demo"}[15m])

   deriv(demo_disk_usage_bytes{job="demo"}[15m])

   predict_linear(demo_disk_usage_bytes{job="demo"}[15m], 3600)
```


9. Aggregations: this is use to show overall result if we want o know 
    
```
   sum(rate(demo_api_request_duration_seconds_count{job="demo"}[5m]))

   sum without(method, status)(rate(demo_api_request_duration_seconds_count{job="demo"}[5m]))

   sum by(instance, path, job)(rate(demo_api_request_duration_seconds_count{job="demo"}[5m]))
```

arithmetic: it give you the ability to easily perform arithmetic between entire sets of time series

```
rate(demo_api_request_duration_seconds_count{job="demo"}[5m])/rate(demo_api_request_duration_seconds_sum{job="demo"}[5m])

rate(demo_api_request_duration_seconds_count{job="demo",status="500"}[5m])/ 
rate(demo_api_request_duration_seconds_count{job="demo"}[5m])
```


