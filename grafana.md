# Installation of Grafana

```
docker run -d -p 3000:3000 --name grafana grafana/grafana:7.5.4
```

## Access grafana on the browser

localhost:3000 of machine ip: 3000

username: admin
pswd == admin

## create a prometheus Datasource

## Create a Dashboard for error 
 a.
  i. title: Errors [rate-5m]
  
  ii. Expression: 

```
 sum without(instance, status)(rate(demo_api_request_duration_seconds_count{job="demo"}[1m]))
```

## Dashboard for lattency

  i. Title: Latency [90th]
  
  ii. Expression:
  
         ```
          histogram_quantile(0.9, sum without(instance, status)(rate(demo_api_request_duration_seconds_bucket{job="demo"}[5m])))
         ```
         
  iii. On the Axes settings in the right menu, set the Unit to seconds (s) under the Time category.


