 DOCKER
  Docker is used to containerize applications. A container is a way to package an app with everything needed to run the app ( App Code + dependencies needed)


 There are different types of container registries
 
  - dockerhub
  - Elastic container registry (ECR)
  - Google container registries


   A Container Runtime is the engine or daemon that runs the container at the background

  EXAMPLES:
          docker
          containerd
          crio
          podman


A container is the running instance of an image ( App code + dependencies)

 The process of building our artifact to image, we need App code, Configurations, dependencies put together using docker


 THE DOCKER ARCHITECTURE CONSIST OF

   1 - docker server   ==> responsible for managing images, starting the image, pulling the image
   2 - docker API      ==> It interacts with the docker server to perform tasks
   3 - docker CLI      ==> It is the command line interface to execute the docker commands

 A DOCKER SERVER IS MADE UP OF

 1 - Container runtime ==> start, stop and pull container
 2 - docker volume     ==> responsible to persist data in a container
 3 - docker network    ==> used for the configuration of docker for communication
 4 - Build images

   * TO INSTALL DOCKER

  * mkdir
  * vi docker.sh

            on the web ==> https://docs.docker.com/engine/install/ubuntu   and cp setup Docker's apt repository

      in the vi docker.sh
      #!/bin/bash   (at the top)
  
      # Add Docker's official GPG key

      back to browser  ===> cp step 2 ( To install the latest version, run)
                       ===> add -y to auto approve


    on the terminal

 -> ls -l docker.sh
 -> change the file to a script using chmod
 ->  ./docker.sh

 Incase the installation cause the daemon to stop

   * systemctl start docker
   * systemctl status docker
   * systemctl enable docker        as a root user


        EVERY CONTAINER IS MADE UP OF
   
1- Filesystem    ==> To store logs ( vitual file system and host file system) 
2- Configuration fie or environment variables  ==> that they can be able to reference)
3- Images

 All images have a "tag" which is the versions of the image

 CONTAINERS RUN ON A HOST ( VM) MADE UP OF

  1 - cgroup   ===> helps to manage resources that containers using
  2 - linux namespace  ===> segregate processes that are running inside the container


 When a container is running it generates data and consumes data

  * host        : has physical filesystem
  * container   : has virtual filesystem


                                     DOCKER COMMANDS


1- docker ps -a                        ===> to check process that are running
2- docker pull                         ===> used in Docker to download an image from a Docker registry, such as Docker Hub, to your local machine.
3- docker run                          ===> is used to create and start a new container from a specified image.
4- docker push                         ===> Docker is used to upload (or "push") an image from your local Docker environment to a Docker registry, such as DOCKERHUB
5- docker start                        ===> to start a container
6- docker stop                         ===> to stop a container
7- docker images                       ===> to see all contaianers that are running/in the system
8- docker rmi id                       ===> used to remove one or more Docker images.
9- docker rm                           ===> used to remove one or more Docker container from the sytem.
10- docker logs                        ===> To check the logs
11-
