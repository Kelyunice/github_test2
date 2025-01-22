BUILD TOOLS
Maven
Graddle
Python
Pypile

       Maven is used for java projects

Maven uses xml language : App codes which is versioned in github


Since maven is used for java projects, we need to install java first and it dependencies
        ``` 
        sudo apt install openjdk-8.jre-headless
        ```
        ```
        sudo apt install maven
        ```

  Maven can be used for :
                       unit test cases
                       compile the codes of java classes
                       validate the code to make sure of the resource structure

 After this then maven will build the APP CODE and DEPENDENCIES into and artifact


When we have build the artifact using MAVEN, we need to store the ARTIFACT in an ARTIFACTORY REPOSITORY(NEXUS)

   THE TWO MAIN COMMANDS IN MAVEN

    ===> mvn package 
    ===> mvn deploy

  * start by cloning your repository
  * check if clone successful ( git status ==> java-maven-app)
  * mvn --version ( to be on maven home directory)
  * configure your setting.xml file ( found in ==> vi /usr/share/maven/conf/setting.xml)
  * configure your pom.xml file ( found in ==> cd java-maven-app/)
  * locate the "Application-java" file found in src dir found in java-maven-app

    TWO MAIN FILES TO CONFIGURE 
     
    ===> pom.xml  : which is where the application codes are stored ( where we configure the nexus address)
    ===> setting.xml  : where we configure our settings to be able to push
    ===> Application  : where the dependencies of the app are found

  
   ==> to locate the formate for our pom.xml file
                 web: https://datacadamia.com/maven/distribution_management/


  IF USING A PUBLIC SERVER LIKE AWS

         CONSIDER CHANGING THE localhost ==> server ip address


 AFTER RUNNING mvn package ==> check if build successful
                               ls ==> you should see target dir

 TO REBUILD

   mvn clean

  BEFORE YOU PUSH TO AN ARTIFACTORY REPOSITORY LIKE NEXUS

  you need to make sure that 
   ===> nexus is up and running
   ===> username and password of the nexus server inmaven has been configured (setting.xml file) 

 TO START AN APP BEFORE DEPLOYING
  ==> java-jar /target/java-maven-app-1
