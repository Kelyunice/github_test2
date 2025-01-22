#JENKINS SETUP AND CONFIGURATION
1- How would you design a jenkins setup for a large-scale enterprise application with multiple teams?
    - Design a master-agent architecture where the master agent handles scheduling and orchestration jobs, and agents execute jobs.
    - Use distributed builds by configuring jenkins agent on different machines or contaainers.
    - Implement folder based multi-tenancy to isolate pipelines for each team.
    - secure the jenkins setup using the role based access control (RBAC)
    - Example: A team has access to folder A with restricted pipeline visibility, while the master node ensures no resource contention.
2- How can you scale jenkins to handle high build loads?
    - Use k8s based Jenkins-agents that scale dynamically based on workload.
    - Implement build queue monitoring and optimize resource allocation by offloading non-critical jobs to low-priority nodes.
    - Use Jenkins Operations Center (CloudBase CI) for centralized management of multiple jenkins instances.
3- How do you manage plugins in a Jenkins environment to ensure stability?
    - Maintain a list oof approved plugins after testing compatibility with the jenkins version.
    - Regurlary update plugins in astaging environment before rolling them into production.
    - Example: While upgrading the git plugin,test it with your pipeline in staging to ensure no disruption.
4- How do you design a Jenkins Pipeline to support multiple environments(e.g Dev, QA and Prod)?
    - Use parameterized pipelines where environment-specific configurations (e.g URLs, credentials) are are passed as parameters.
    - Implement environment-specific stages or branch specific pipelines.
    - Example A pipleine that promotes a build from Dev to QA and then to Prod using approval gates between stages.
5- How can you handle dynamic branch creation in Jenkins pipelines?
    - Using multibranch pipelines that automatically detect new branches in a repository and creates pipelines for them.
    - Configure the Jenkinsfile in each branch to define its pipeline behavior
6- How do you ensure pipeline resilience in case of intermitent failures?
    - Use retry blocks in declarative or scripted pipelines to retry failed stages.
    - Example Retrying a flaky test stage three times with exponential backoff.
    - Implement conditional steps using CATCHERROR to handle faillures gracefully.
             #SECURITY AND ACCESS CONTROL
7- How do you secure sensitive credentials in jenkins pipeline?
    - Use the jenkins credentails plugins to store secrets securely.
    - Access credentials using environment variables or bindings in the pipeline.
    - Examples Fetch an API key stored in jenkins credentails using WITHCREDENTIALS in ascripted pipeline.
8- How do you enforce Role Based Access Control (RBAC) in jenkins?
    - Use the Role-Based authorization strategy plugin.
    - Define roles like Admin, Developer, and Viewer , and assign permissions for jobs, folders, and builds accordingly.


            #INTERGRATION WITH TOOLS
9- How do you intergrate jenkins with Docker for Building applications.
    - Use the Docker plugin or Docker pipeline plugin
    - Example : Build a docker image inthe pipeline using (docker.build ) and push to a container registry.
    - Run test in ephemeral docker containers for consistent test environments.
10- How do you intergrate Jenkins with a K8s cluster for deployments?
    - Use the K8s plugin on kubectl commands in the pipeline.
    - EXAMPLE:Use the k8s pod template with customcontainers for builds, the deploy apllications using (kubectl apply)

          JOB OPTIMIZATION AND PERFORMANCE
11- How can you reduce the build time of a jenkins job?
    - Use parallel stages to execute independent task simultanously.
    - Example: Parallel static code analysis, unit tests, and intergration tests.
    - Use build caching mechanism like Docker layer caching or dependency caching.
12- How do you optimize jenkins for CI/CD pipelines with heavy test loads?
    - Split tests into smaller batches and run them in parallel.
    - Use sharding for distributed test execution across multiple agents.
    - Example: Divide a 10,000-test suite into 10 shards and distribute them across agents.


        REAL-WORLD TROUBLESHOOTING
13- What would you do if a jenkins job hangs indefinitely?
    - Check the jenkins build logs for deadlocks or resource contention.
    - Restart the agent where the build is stuck, if needed.
    - Example: A job stuck in (docker build) could  indicate a daemon issues;restart the Docker service.
14- How do you troubleshoot a jenkins job that keeps failing at the same step?
    - Analyse the console output to identify the error message.
    - Check for environmental issues like missing dependencies or incorrect permissions.
    - Example: A maven build failing due to repository connectivity might require checking proxy configurations.


       ADVANCED PIPELINE SCENARIO
15- How do you implement manual approval gates in jenkins pipelines?
    - Use the (input) step in a declarative pipeline.
    - Example: Add an approval step before deploying to production. Only after manual confirmation does the pipeline proceed.
16- How do you handle blue-green deployments in jenkins?
    - Create seperate pipelines for blue and green environments.
    - Route traffic to the new environment after successful deployment and health checks.
    - Example: Use AWS Route3 or k8s Ingress to switch traffic seamlessly.


          MONITORING AND REPORTING
17- How do you monitor jenkins build trends?
    - use the build history and build monitor plugins.
    - Example: Visualize pass/fail trends over time to identify flaky tests.
18- How do you notify teams about build failures?
    - Use the Email extension or Slack Notification plugins.
    - Example: Configure a Slack webhook to notify the (#build-alerts) channel upon failure


                VERSIONS CONTROL SYSTEM INTERGRATION
19- How do you manage monrepos in jenkins pipelines?
    - Use Spare chekouts to fetch only the required directories.
    - Example: Trigger pipelines based on changes in specific subdirectories using the (dir) parapeter in Git.
20- How do you handle merge conflicts ina a jenkins pipeline?
    - use (Git pre-merge hooks) or resolve conflicts locally and push the updated code.
    - Example: A pipeline can fetch both source and target branches, merge them in a temporary brannch, and check for conflicts.


              ADVANCED PIPELINE DESIGN
21- How do you trigger a jenkins pipeline from another pipeline?
    - use the (build ) step in a declarative or scripted pipeline to trigger another pipeline.
    - Example: Pipeline A builds the application, and pipeline B deploys it. Pipeline A calls pipeline B using 
         (build(job: 'Pipeline-B',parameters: (string(name: 'version',value: '1.0'))).
22- How do you handle shared libraries in jenkins pipelines?
    - Use the ( Global Shared Libraries) feature in jenkins.
    - Example: Create reusable Groovy functions for common tasks (e.g linting, packaging) and call them in pipeline using ( @Library('my-library').
23- How do you implement conditional ogic in jenkins pipelines?
    - Use (When) in declarative pipelines or (if) statements in scripted pipelines.
    - Example: Skip deployment if the branch is not (main) using (when){branch 'main'}.

            ERROR HANDLING AND RECOVERY
24- How do you handle job failures in a Jenkins Pipeline?
    - Use the (catchError) block to handle errors gradualy
    - Example:

              catchError{
               sh 'some-faclling-command'
              }
              echo 'Handled the failure and oroceeding.'

25- How would you do if a jenkins master node crashes?
    - Restore the master node from backups.
    - Use jenkins' thinbackup or a similar plugin for automated backups.
    - Example: After restoration, ensure the plugin and configuration are synchronized.
26- How do you restart a failed jenkins pipeline from a specific stage?
    - Enable the (Restart from stage) feature in the jenkins declarative pipeline.
    - Example: If the (Deploy) stage fails, restart the pipeline from that stage without re-executing previous stages.


             TESTING AND QUALITY ASSURANCE
27- How do you intergrate jenkins with Sonarqube for code quality analysis?
    - Use the SonarQube Scanner plugin.
    - Example: Add a stage in the pipeline to run (sonar-scanner) and publish results to the SonarQube server.
28- How do you enforce code coverage thresholds in jenkins pipelines?
    - Use tools like (JaCoCo or Cobertura) and configure the build to fail if thresholds are not met.
    - Example

              jacoco(execPattern: '**/jacoco.exec',minimumBranchCoverage: '80')


             PARALLELISM AND OPTIMIZATION
29- How do you implement parallelism in jenkins pipelines?
    - use the (parallel) directive in declarative pipeline or parallel block in scripted pipelines.
    -  Example: Run (unit tests, intergration tests, and linting in parallel stages.
30- How do you optimize resource utilization in jenkins?
    -  Use (lock) to manage resource contention.
    - Example: Limit concurrent jobs accessing a shared environment using 
            lock('resourceName').

               CONTAINERIZED BUILDS
31- How do you run jenkins job in a Docker container?
    - Use the (docker) block in declarative pipelines.
    - Example:
              agent{
               docker{image 'node:14'}
              }
32- How do you ensure consistent environments for jenkins builds?
    - use docker images to define build environments.
    - Example: use a prebuild image with all dependencies pre-installed for faster builds.


              INTERGRATION WITH CLOUD PLATFORMS
33- How do you integrate jenkins with AWS for CI/CD?
    - Use the AWS CLI or AWS-specific jenkins plugins.
    -Example: Deploy an application to s3 using (aws s3 cp) commands in the pipeline.
34- How do you configure jenkins to deploy to Azure k8s service (AKS)?
    - Use (kubectl) commands with AKS credentials stored in jenkins credentials.
    - Example: 
               Deploy manifests using (sh 'kubectl apply -f k8s.yaml'.


             JOB AND PIPELINE TRIGGERING
35- how do you trigger a jenkins job when a file changes in Git?
     - Use GitHub or Bitbucket webhooks configured with the jenkins job.
     - Example:
               A webhook triggers the job only for changes in a specific folder by setting path filters.
36- How do you schedule periodic builds in jenkins?
     - Use the (Build periodically) option or (cron) syntax in pipeline scripts.
     - Example:
                schedule a nighty build using HO***


               AUDIT AND COMPLIANCE
37- How do you audit build logs and job execution in Jenkins?
    - Enable the Audit Trial plugin to track user actions.
    - Example: View changes made to jobs, buids, and plugins.
38- How do you implementcompliance checks in jenkins pipelines?
    - Integrate with tools like OpenSCAP or custom scripts for compliance validation.
    - Example:Validate infrastructure as codeIaC templates for compliance before deployment.


               BUILD ARTIFACTS AND RELEASES
39- How do you manage artifacts in Jenkins?
    - Use the ( Archive the artifacts) post-build steps.
    - Example: Store JAR files and logs for future reference using (archiveArtifactsartifacts: 'build/*.jar'.
40- How do you publish artifacts to a repository like Nexus or Artifactory?
    - Use Maven/Gradle plugin or REST APIs for publishing.
    - Example: Push a JAR file to Nexus with 
                                             sh'mvn deploy'


              NOTIFICATIONS AND ALERTS
41- How do you notify a team about pipeline status?
    - Use slack or email plugins for notifications
    - Example: Notify slack on success or failure with:
               slackSend channel:'#builds',message:"Build #$(env.BUILD_NUMBER)${currentBuild.result}'
42- How do you send detailed build reports via email in jenkins?
    - use the emailExtension plugin and configuration templates for detailed reports
    - Example: Include build logs and test results in the email.


              BACKUP AND DISASTER RECOVERY
43- How do you back up Jenkins configurations?
    - Use the (thinbackup) plugin or manual backup of $JENKINS_HOME.
    - Exaple: Automate backups nightly and store them in a secure location like s3
44- How do you recover a jenkins instance from backup?
    - Restore the $JENKINS_HOME directory from the backup and restart jenkins.
    - Example: After restoration,validate all jobs and credentails.


              ADVANCED USE CASES
45- How do you implement feature flags in jenkins pipelines?
    - use environment variables or external tools like lanchDarkly.
    - Example: A featureflag determines whether to deploy the feature branch.
46- How do you intergrate Jenkins with a database for testing?
    - spin up a database container or use a preconfigured test database.
    - Example: Use Docker compose to bring up a MySQL container before running tests.


              REAL_WORLD CHALLENGES
47- How do you manage long-running jobs in Jenkins?
    - Break them into smaller jobs or stages to allow checkpoints.
    - Example: Use (timeout) to terminate excessively long builds.
48- What would you do if Jenkins pipelines start failing intermittently?
    - Investigate resource constraints, flaky tests, or network issues.
    - Example: Monitor agent logs and rebuild affected stages.
49- How do you manage Jenkins jobs for multiple branches in a monorepo?
    - Use multibranch pipelines or branch-specific Jenkinsfiles.
50- How do you handle cross-team collaboration in Jenkins pipelines?
    - Use shared libraries for reusable code and maintain a central Jenkins governance team.


            SCALING AND RESOURCE MANAGEMENT
51- How do you manage Jenkins agents in a dynamic cloud environmrnt?
    - use a cloud provider plugin (e.g Amazon EC2 or k8s).
    - Example: Configure k8s-based agents to dynamically spin up pods based on job demands.
