 NEXUS ( nuGet Gallery, Maven central)

Nexus is an open source artifactory Tool used to store and retrieve artifacts.

It uses Jar files
        war files
        Zip files
        docker imaages

          A REPSOTORY MANAGER

This allows us to upload and store different built in artifact and we can retrieve and download them later( wharehouse to store software parts)

We have PUBLIC and PRIVATE repo managers

                 BENEFITS
  1 - It enalbes  a better collaboration
  2- It increases our build performance.


   TPYES OF NEXUS REPOSITORY

  1 - Proxy            : Its a link to the remote repo
  2 - Hosted           : Maven snapshot - Artifact which are not yet stable
                         Maven releases -  stable and ready for production
  3 - Repository Groups: Contain group of repo that can be contained together.

   * NEXUS INSTALLATION (To Run Nexus as a container)

   -  sudo apt update
   -  intall docker 

        ( go on dockerhub and cp smartype image)
   - Run it
   - docker ps
   - docker exec -it
   - docker stop
   - docker rmi id ==> to delete an image
  
   YOU NOW GO TO THE BROWSER AND LOOK FOR THE LOCALHOST


   TO GET THE PATH TO USE TO LOGIN

  -  docke volume ls
  - nexus-data
  - docker volume inspect nexus-data
  - docker ps
  - docker exec -it id /bin/bash
  - ls /
  - ls /nexus-data


   AS A REGULA USER
          sudo ls /var/lib/docker/volumes/nexus-data
          sudo ls /var/lib/docker/volumes/nexus-data/ _data
          sudo cat /nexus-data/admin.password
             
    AS AN ADMIN
  - nexus-snapshot
  - copy the url

   THE PASSWORD CREATED IN NEXUS ADMIN AFTER LOGIN IS THESAME PASWORD TO BE USED ON THE settings.xml file


      * The 2 MOST IMPORT FILES TO CONFIGURE ARE
                   
   1 - setting.xml 
   2 - pom.xml ( you will need the manifest file) ( the file in the maven home dir ===> java-maven-app)
              https://datacadamia.com/maven/distribution_management


    * RUN THE COMMAND 
                     mvn deploy

   To push to another repository we need to get another permission which needs to be configured in Nexus (user) and (role) before you can push ( mvn deploy)

   * Sign in to nexus
                     user -  permission ===> active
                     roles - priveleges ( nexus-repo-view-maven2-maven-snapshot)
                      You caan dd additional priveleges

    
     * mvn validate 
     * mvn test
     * mvn compile

  * To check if image/arifact is working
    curl -u admin:password -x GET 'http://localhost:8081/service/rest/v1/repositories'

     docker stop id
     docker rm id
     docker images
     docker rmi
