# Docker Crash Course for Java Developers

## Learn Docker creating containers for Spring Boot APIs and Microservices

Learn Docker Fundamentals? Yes.   Create Containers for Microservices? Yes.     Create Containers for Full Stack Applications? Yes. Of Course. Hands-on? Of course.

Do you have ZERO experience with Docker? No Problem.

Do you want to learn to create containers for Java Spring Boot Applications and Microservices using Docker with an easy to learn, step by step approach?

Are you ready to learn about Docker and take the next step in your programming career?

Do you want to join 300,000+ learners having Amazing Learning Experiences with in28Minutes?

Look No Further!

## Getting Started
- [Video - Spring in 10 Steps](https://www.youtube.com/watch?v=edgZo2g-LTM)
- [Video - Spring Boot in 10 Steps](https://www.youtube.com/watch?v=pcdpk3Yd1EA)
- [Video - JPA/Hibernate in 10 Steps](https://www.youtube.com/watch?v=MaI0_XdpdP8)
- [Video - React in 10 Steps](https://www.youtube.com/watch?v=SWXuXhZkNQc&t=110s)
- [Article - Getting started with React and Spring Boot - Full Stack](https://www.springboottutorial.com/spring-boot-react-full-stack-crud-maven-application)
- [Article - Using Spring Security and JWT with React and Spring Boot](https://www.springboottutorial.com/spring-boot-react-full-stack-with-spring-security-basic-and-jwt-authentication)

#### Required Tools
- Docker
- Git
- Node v8+ for npm
- Visual Studio Code - Latest Version
- Java 8+
- Eclipse - Oxygen+ - (Embedded Maven From Eclipse)
- Docker Editor Plugin - https://marketplace.eclipse.org/content/docker-editor

#### Installing Guides

- [Playlist - Installing Java, Eclipse & Embedded Maven](https://www.youtube.com/playlist?list=PLBBog2r6uMCSmMVTW_QmDLyASBvovyAO3)
- [Playlist - Installing Node Js (npm) & Visual Studio Code](https://www.youtube.com/playlist?list=PLBBog2r6uMCQN4X3Aa_jM9qVjgMCHMWx6)

#### Troubleshooting Installations
- Node JS and NPM 
  - https://docs.npmjs.com/common-errors
  - https://docs.npmjs.com/getting-started/troubleshooting
- Visual Studio Code
  - https://code.visualstudio.com/docs/supporting/errors
  - https://code.visualstudio.com/docs/supporting/FAQ
- Eclipse and Embedded Maven
  - Troubleshooting Guide - https://github.com/in28minutes/in28minutes-initiatives/tree/master/The-in28Minutes-TroubleshootingGuide-And-FAQ#tip--troubleshooting-embedded-maven-in-eclipse
  - PDF - https://github.com/in28minutes/SpringIn28Minutes/blob/master/InstallationGuide-JavaEclipseAndMaven_v2.pdf
  - GIT Repository For Installation - https://github.com/in28minutes/getting-started-in-5-steps

#### Troubleshooting Docker

- Problem - Caused by: com.spotify.docker.client.shaded.javax.ws.rs.ProcessingException: java.io.IOException: No such file or directory
- Solution - Check if docker is up and running!
- Problem - Error creating the Docker image on MacOS - java.io.IOException: Cannot run program “docker-credential-osxkeychain”: error=2, No such file or directory
- Solution - https://medium.com/@dakshika/error-creating-the-docker-image-on-macos-wso2-enterprise-integrator-tooling-dfb5b537b44e



## Course Overview

******* Course Overview *******

Pivotal Cloud Foundry (PCF) provides a great cloud native platform to deploy Spring Boot Applications.

Spring Boot is the No 1 Java Framework to develop REST API and Microservices. 

In this course, we deploy a variety of Spring Boot Applications to the Cloud:
- REST APIs - Hello World and Todo - Jar
- Todo Web Application War
- Full Stack Application with React and Spring Boot
- CCS and CES Microservices
- Route Services

This course would be a perfect first step as an introduction to PCF and the Cloud.

You will be using deploying a variety of projects to Pivotal Cloud Foundry (PCF) . These projects are created with  React (Frontend Framework), Spring Boot (REST API Framework), Spring (Dependency Management), Spring Security (Authentication and Authorization - Basic and JWT), BootStrap (Styling Pages), Maven (dependencies management), Node (npm), Visual Studio Code (TypeScript IDE), Eclipse (Java IDE) and Tomcat Embedded Web Server. We will help you set up each one of these.

## What you'll learn
- You will Learn the Fundamentals of Pivotal Cloud Foundry ( PCF ) from Zero, no previous experience required
- You will learn to deploy Spring Boot REST API to Pivotal Cloud Foundry ( PCF )
- You will learn to deploy Java, Spring Boot Full Stack Applications to Pivotal Cloud Foundry ( PCF )
- You will be using a number of PCF Services - Databases, Spring Cloud Services including Service Registry, Config Server and Hystrix . 
- You will learn how to Auto Scale applications based on load as well as deploy multiple instances behind a load balancer using Pivotal Cloud Foundry.
- You will Join 250,000 Learners having AMAZING LEARNING Experiences with in28Minutes

## Requirements
- You have an attitude to learn while having fun :)
- You have some programming experience with Java, Spring and Spring Boot
- You DO NOT need to have any experience with Pivotal Cloud Foundry
- We will help you install Eclipse, Visual Studio Code, Git client, Docker Desktop and Node JS (for npm)

## Who is this course for
- You are a Java Spring Boot developer getting started with the Cloud
- You want to get your Java applications deployed to PCF (Pivotal Cloud Foundry) Quickly
- You are a Java Developer and You are curious about PCF and the Cloud
- You want to learn to deploy a Java Spring Boot full stack application to PCF (Pivotal Cloud Foundry) 
- You want to learn to deploy Spring Boot Microservices with Service Registry, Config Server, Distributed Tracing and Load Balancing to PCF (Pivotal Cloud Foundry) 

## Step By Step Details



```sh
for file in *; do mv "${file}" "${file//-/ }"; done
for file in *; do mv "${file}" "${file//   / - }"; done
for file in *; do mv "${file}" "${file//01 Step/Step}"; done
```

## Diagrams

- Courtesy http://viz-js.com/

```
graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=3]

Containers, LocalImages [height=1]

DockerClient -- Daemon
Daemon -- Containers 
Daemon -- LocalImages
Daemon -- ImageRegistry

DockerClient[label=<Docker Client>]
ImageRegistry[label=<Image Registry <BR /><FONT POINT-SIZE="10">nginx<BR />mysql<BR />eureka<BR />your-app<BR /><BR /></FONT>>];
Daemon[label=<Docker Daemon>]


}


graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2]
Hypervisor,HostOS, Hardware[shape=record, width=6.5, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];

Application1 -- Software1 [style=invis]
Application2 -- Software2 [style=invis]
Application3 -- Software3 [style=invis]

Software1 -- GuestOS1 [style=invis]
Software2 -- GuestOS2 [style=invis]
Software3 -- GuestOS3 [style=invis]
GuestOS1 -- Hypervisor [style=invis]
GuestOS2 -- Hypervisor [style=invis]
GuestOS3 -- Hypervisor [style=invis]
Hypervisor -- HostOS [style=invis]
HostOS -- Hardware [style=invis]

}


graph architecture {

node[style=filled,color="#59C8DE"]
//node [style=filled,color="#D14D28", fontcolor=white];
rankdir = TB
node[shape=record, width=2]
HostOS, CloudInfrastructure, DockerEngine[shape=record, width=6.5, style=filled,color="#D14D28", fontcolor=white]
edge [width=0]
graph [pad=".75", ranksep="0.05", nodesep="0.25"];
Container1,Container2,Container3[height=2]

Container1 -- DockerEngine [style=invis]
Container2 -- DockerEngine [style=invis]
Container3 -- DockerEngine [style=invis]
DockerEngine -- HostOS [style=invis]
HostOS -- CloudInfrastructure [style=invis]

}
```

## Docker Commands from other courses

```
docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 mysql:5.7

mysqlsh
\connect todos-user@localhost:3306
\sql
use todos
select * from todos;

docker container list
docker stop 9a8dfcfa01d4
docker rm 9a8dfcfa01d4

docker run --publish 8200:80 in28min/aws-hello-world-rest-api:0.0.1-SNAPSHOT
docker login

docker push @@REPO@@/aws-hello-world-rest-api:0.0.1-SNAPSHOT

docker run --publish 8000:8000 --network currency-network --name=currency-exchange-service in28min/aws-currency-exchange-service-h2:0.0.1-SNAPSHOT

docker run --publish 8100:8100 --network currency-network --env CURRENCY_EXCHANGE_URI=http://currency-exchange-service:8000 in28min/aws-currency-conversion-service:0.0.1-SNAPSHOT

docker images
docker container ls
docker container ls -a

docker container start fed549e69e9d
docker container stop tender_ardinghelli
docker container stop c165f459e7d7
docker container logs c165f459e7d7
docker container logs c165f459e7d7 //Whats the option to tail the logs?
docker container rm fed549e69e9d
docker container prune
docker container inspect 0967ba7aa180

docker images
docker image history f8049a029560
docker image history in28min/todo-rest-api-h2
docker image inspect 01-hello-world-rest-api:0.0.1-SNAPSHOT
docker image remove f8049a029560

#1
mvn clean install
docker build .
mvn clean install -DskipTests
docker images
docker run -p 8080:8080 b192c2f856e0

mvn compile jib:build -Dimage=in28minutes/test
mvn compile jib:dockerBuild -Dimage=in28minutes/test
After adding configuration - mvn -X package -DskipTests

docker images --format "table {{.Repository}}\t{{.Tag}}\t{{.CreatedSince}}"
docker pull in28min/aws-currency-exchange-service-h2:0.0.1-SNAPSHOT
docker container ls --format='{{json .}}'
docker image ls --format='{{json .}}'
docker image ls --format='{{.Containers}} {{.Tag}}'
  
docker system prune
docker system prune -a
docker image prune
docker container prune
docker network prune

docker network ls
docker container ls
docker volume ls

docker network create currency-network
docker run -p 8000:8000 --network currency-network --name currency-exchange-service c047b15426b8
docker run -p 8000:8000 --network currency-network --name currency-exchange-service c047b15426b8
docker run -p 8100:8100 --network currency-network -e CURRENCY_EXCHANGE_URI=http://currency-exchange-service:8000 f1
```

## Next Steps

## Todo
- Use UNIX Containers on Windows
- --link
- play-with-docker.com
- Plugins - JIB, Fabric 8
- Network Types
- Volumes
  - Accessing host device in container `--device=HOST_PATH:CONTAINER_PATH`
  - Persisting data using volumes. `create volume customvol` `-v customvol:/data` `docker volume inspect`
  - Share Data between Host and container `-V $(HOME)/data_share:/data`
- Fabric8 Plugin
  - https://stackabuse.com/dockerizing-a-spring-boot-application/
- Pushing an Image
  - You need Registry, Repository and Tag
  - docker image build -t web:latest .  (If you push this, you will get an error. Because you need to specify a repository)
  - docker image build -t in28min/web:latest .
  - docker image push
  - docker.io/in28min/spring-boot:1.0.0.SNAPSHOT
  -   DEFAULT   REPOSITORY          TAG  
- Commands
  - docker system prune
  - docker system prune -a
  - docker image prune
  - docker container prune
  - docker network prune
  - docker network ls
  - docker container ls
  - docker volume ls
  - docker events
  - docker stats
- Create Auto Build -> Github & Docker Hub

### Misc

- Course Creation
- Post Course Creation
  - Make Github Repo Public
  - Course Promotion Emails/Posts
    - 1 Emails on Udemy
    - 1 Emails to Email List
  - Create YouTube Course Preview Video
    - Add YouTube Course Preview Video as End Video for all videos
    - Make it the YouTube Default Video
  - Release atleast 20 small videos - one a day on Youtube
  - Do atleast 3 Youtube live sessions
  - After a Month
    - UFB and Packt


### Commands Executed during the course

```
  481  docker container ls
  482  docker container exec unruffled_tereshkova ls /tmp
  483  docker container cp target/hello-world-rest-api.jar 54cf414254e48d5f68c4d468b2dd4cbdd95d17f9e2074fdb9df7f64987697f2b:/tmp
  484  docker container exec unruffled_tereshkova ls /tmp
  485  docker container commit unruffled_tereshkova in28min/hello-world-rest-api:manual 
  486  docker run -p 8080:8080 in28min/hello-world-rest-api:manual
  487  docker run -p 8080:8080 in28min/hello-world-rest-api:manual
  488  docker container
  489  docker container ls
  490  docker container commit --change='CMD ["java","-jar","/tmp/hello-world-rest-api.jar"]'
  491  docker container commit unruffled_tereshkova --change='CMD ["java","-jar","/tmp/hello-world-rest-api.jar"]'
  492  docker container commit unruffled_tereshkova --change='CMD ["java","-jar","/tmp/hello-world-rest-api.jar"]'
  493  docker container commit --change='CMD ["java","-jar","/tmp/hello-world-rest-api.jar"]' unruffled_tereshkova in28min:hello-world-rest-api:manual2
  494  docker container commit --change='CMD ["java","-jar","/tmp/hello-world-rest-api.jar"]' unruffled_tereshkova in28min/hello-world-rest-api:manual2
  495  docker run -p 8080:8080 in28min/hello-world-rest-api:manual2
  496  docker inspect in28min/hello-world-rest-api:dockerfile1
  497  docker history in28min/hello-world-rest-api:dockerfile1
  533  docker container ls -l
  534  docker container ls
  535  docker volume ls
  536  clear
  537  open .
  538  docker build -t in28min/hello-world-rest-api:dockerfile1 .
  539  docker container ls
  540  docker container stop 8a0d79c6b154
  541  docker run -p 8080:8080 in28min/hello-world-rest-api:dockerfile1
  542  clear
  543  docker history in28min/hello-world-rest-api:dockerfile1
  544  docker run -p 8080:8080 in28min/hello-world-rest-api:dockerfile1
  545  docker build -t in28min/hello-world-rest-api:dockerfile1 .
  546  clear
  547  docker run -p 8080:8080 in28min/hello-world-rest-api:dockerfile1
  548  clear
  549  docker history in28min/hello-world-rest-api:dockerfile1
  550  clear
  551  docker history help
  552  docker history --help
  553  clear
  554  docker history in28min/hello-world-rest-api:dockerfile1
  555  docker build -t in28min/hello-world-rest-api:dockerfile1 .
  556  docker build -t in28min/hello-world-rest-api:dockerfile1 .
  557  docker build -t in28min/hello-world-rest-api:dockerfile1 .
  558  clear
  559  pwd
  560  mvn package -DskipTests
  561  docker container ls
  562  docker run -p 8080:8080 in28min/hello-world-rest-api:0.0.1-SNAPSHOT
  563  mvn package -DskipTests
  564  docker run -p 8080:8080 in28min/hello-world-rest-api:0.0.1-SNAPSHOT
  565  open .
  566  mvn package -DskipTests
  567  mvn clean package -DskipTests
  568  mvn clean package -DskipTests
  569  mvn clean package -DskipTests
  570  mvn clean package -DskipTests
  571  mvn clean package -DskipTests
  572  mvn clean package -DskipTests
  573  mvn clean package -DskipTests
  574  mvn clean package -DskipTests
  575  ls
  576  docker images
  577  docker inspect in28min/hello-world-rest-api:0.0.1-SNAPSHOT
  578  clear
  579  docker history in28min/hello-world-rest-api:0.0.1-SNAPSHOT
  580  docker images
  581  clear
  582  mvn clean package -DskipTests
  583  docker container ls
  584  clear
  585  docker run -p 8080:8080 in28min/hello-world-rest-api:0.0.1-SNAPSHOT
  586  clear
  587  mvn clean package -DskipTests
  588  clear
  589  docker run -p 8080:8080 in28min/hello-world-rest-api:0.0.1-SNAPSHOT
  590  docker history in28min/hello-world-rest-api:0.0.1-SNAPSHOT
  591  docker inspect ENTRYPOINT ["sh" "-c" "ja…   0B                  
b35b36685158        About a minute ago   /bin/sh -c #(nop) ADD file:d486f433c28daeab7…   16.8MB              
  592  clear
  593  docker run -p 8080:8080 in28min/hello-world-rest-api:0.0.1-SNAPSHOT
  594  clear
  595  mvn clean package -DskipTests
  596  mvn clean package -DskipTests
  597  docker history in28min/hello-world-rest-api:0.0.1-SNAPSHOT
  598  mvn docker:build
  599  docker images
  600  docker run -p 8080:8080 webservices/01-hello-world-rest-api
  601  docker images
  602  mvn docker:run
  603  mvn docker:build
  604  mvn clean install -DskipTests
  605  mvn clean install -DskipTests
  606  mvn clean install -DskipTests
  607  mvn clean package -DskipTests
  608  docker images
  609  mvn clean install -DskipTests
  610* 
  611  mvn clean package -DskipTests
  612  docker images
  613  clear
  614  docker build -t in28min/hello-world-rest-api:dockerfile1 .
  615  open .
  616  docker build -t in28min/hello-world-rest-api:dockerfile1 .
  617  docker build -t in28min/hello-world-rest-api:dockerfile1 .
  618  open .
  619  clear
  620  mvn clean package
  621  clean
  622  clear
  623  docker build -t in28min/hello-world-rest-api:dockerfile1 .
  624  mvn clean package -DskipTests
  625  docker build -t in28min/hello-world-rest-api:dockerfile1 .
  626  clear
  627  mvn clean package -DskipTests
  628  docker history 01-hello-world-rest-api:0.0.1-SNAPSHOT
  629  docker images
  630  clear
  631  docker history 01-hello-world-rest-api:0.0.1-SNAPSHOT
  632  mvn clean package -DskipTests
  633  docker history 01-hello-world-rest-api:0.0.1-SNAPSHOT
  634  clear
  635  docker history 01-hello-world-rest-api:0.0.1-SNAPSHOT
  636  docker run -p 8080:8080 01-hello-world-rest-api:0.0.1-SNAPSHOT

    498  pwd
  499  cd ../01-hello-world-rest-api/
  500  ls
  501* 
  502  mvn clean package -DskipTests
  503  docker images
  504  mvn docker:build
  505  mvn docker:build
  506  mvn clean package -DskipTests
  507  mvn clean package -DskipTests
  508  mvn clean package -DskipTests
  509  docker images
  510  docker run -p 8080:8080 01-hello-world-rest-api
  511  mvn clean package docker:build
  512  mvn clean package docker:build
  513  docker run -dit 51297c224d60
  514  docker container exec 7714 ls /maven
  515* docker run -p 8080:8080 01-hello-world-rest-api:latest
  516  docker container ls
  517  docker stop 7714
  518* docker container ls[A
  519  clear
  520  mvn clean package -DskipTests
  521  docker run -p 8080:8080 01-hello-world-rest-api:latest
  522  docker images
  523  clear
  524  cd ../02-todo-web-application-h2/
  525  pwd
  526* docker buil
  527  mvn clean package
  528  clear
  529  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT
  530  mvn clean package -DskipTests
  531  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT
  532  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT
  533  mvn clean package -DskipTests
  534  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT
  535  mvn clean package -DskipTests
  536  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT
  537  docker run -p 8080:8080 in--cmd debug 28min/todo-web-application-h2:0.0.1-SNAPSHOT
  538  docker run -p 8080:8080 --cmd debug 28min/todo-web-application-h2:0.0.1-SNAPSHOT
  539  docker run -p 8080:8080 -c debug 28min/todo-web-application-h2:0.0.1-SNAPSHOT
  540  docker run --help
  541  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT debug
  542  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT catalina.sh debug
  543  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT catalina.sh run
  544  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT catalina.sh start
  545  docker image
  546  docker container ls
  547  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT catalina.sh start
  548  docker container ls
  549  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT ping google.com
  550  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT catalina.sh run -security
  551  docker images
  552  docker run in28min/hello-world-rest-api:dockerfile1 test
  553  docker run -d in28min/hello-world-rest-api:dockerfile1 test
  554  docker container ls
  555  docker container stop a75
  556  clear
  557  docker run -p 8080:8080 in28min/todo-web-application-h2:0.0.1-SNAPSHOT ping google.com
  558  docker container ls
  559  clear
  560* docker run -p 8080:8080 in28min/todo-web-application-h2:
  561  clear
  562  docker run -p 8080:8080 in28min/hello-world-rest-api:dockerfile1 param1 param2
  563  clear
  564  pwd
  565  cd ../03-todo-web-application-mysql/
  566  pwd
  567  mvn clean package -DskipTests
  568  docker run -p 8080:8080 in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  569  docker run -p 8080:8080 --network host in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  570  docker run -p 8080:8080 --network host --name=todo-web-application in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  571  docker run -p 8080:8080 --link=mysql --e RDS_HOSTNAME=mysql in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  572  docker run -p 8080:8080 --link=mysql --env RDS_HOSTNAME=mysql in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  573  docker run --rm -d --network host --name my_nginx nginx
  574  echo $DOCKER_HOST
  575  echo $DOCKER_HOST
  576  docker
  577  docker container list
  578  docker inspect 0882e1f6ac9c
  579  docker network ls
  580  docker inspect e287a8868c75
  581  docker ps
  582  ifconfig
  583  docker run -p 8080:8080 --network=host  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT ping http://localhost:8080 
  584  docker run -p 8080:8080 --network=host  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT ping http://localhost:80 
  585* docker run -p 8080:8080 --network=host  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT ping http://:80 
  586  clear
  587  docker ls
  588  docker container ls
  589  docker stop 0882e1f6ac9c
  590  clear
  591  ping host.docker.internal
  592  docker run -p 8080:8080 --network=host  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT ping host.docker.internal
  593  docker run --rm -d --network host --name my_nginx nginx
  594  docker run -p 8080:8080 --network=host  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT curl host.docker.internal
  595  docker run -p 8080:8080 --network=host  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT curl http://192.168.65.2
  596  docker run -p 8080:8080 --network=host  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT ping http://192.168.65.2
  597  docker run -p 8080:8080 --network=host  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT ping host.docker.internal
  598  clear
  599  docker container ls
  600  docker container stop dd6cb601c08b
  601  docker container ls
  602  mvn clean package -DskipTests
  603  docker container run -p 8080:8080 in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  604  docker container ls
  605* docker container run --network=none in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  606  clear
  607  docker network ls
  608  docker inspect bridge
  609  docker container run -p 8080:8080 --link=mysql -e RDS_HOSTNAME=mysql  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  610  clear
  611  docker network ls
  612  docker network create web-application-mysql-network
  613  docker containers
  614  docker container ls
  615  docker container stop 5d0737ecd47a
  616  docker container ls
  617  clear
  618  docker network ls
  619  docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network mysql:5.7
  620  docker rm mysql
  621  docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network mysql:5.7
  622  docker container run -p 8080:8080 --network=web-application-mysql-network -e RDS_HOSTNAME=mysql  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  623  history
  624  clear
  625  docker container restart mysql
  626  docker container run -p 8080:8080 --network=web-application-mysql-network -e RDS_HOSTNAME=mysql  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  627  clear
  628  docker container ls
  629  docker container stop 56
  630  docker container stop 5661
  631  docker container ls
  632  docker container prune
  633  clear
  634  docker container ls -a
  635  docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network mysql:5.7
  636  docker container run -p 8080:8080 --network=web-application-mysql-network -e RDS_HOSTNAME=mysql  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  637  docker container ls
  638  docker container stop cc
  639  clear
  640  docker container ls
  641  docker container prune 
  642  clear
  643  docker container run -p 8080:8080 --network=web-application-mysql-network -e RDS_HOSTNAME=mysql -d in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  644  docker container logs -f 91a 
  645  clear
  646  docker container ls
  647  docker container stop 91
  648  docker container prune
  649  clear
  650  docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network mysql:5.7
  651  docker container ls
  652  docker container run -p 8080:8080 --network=web-application-mysql-network -e RDS_HOSTNAME=mysql -d in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  653  docker container logs -f ad70
  654  docker container ls
  655  docker container restart mysql
  656  docker container ls
  657  docker container stop mysql
  658  docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network mysql:5.7
  659  docker rm mysql
  660  docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network mysql:5.7
  661  docker container ls
  662  docker container logs ad7
  663  docker container ls
  664  docker stop ac
  665  docker stop ad
  666  docker container prune
  667  clear
  668  docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network --volume mysql-database-volume:/var/lib/mysql  mysql:5.7
  669  docker container run -p 8080:8080 --network=web-application-mysql-network -e RDS_HOSTNAME=mysql -d in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
  670  docker container logs 4e9
  671  docker container logs -f 4e9
  672  clear
  673  docker container ls
  674  docker stop mysql
  675  docker rm mysql
  676  docker container ls -a
  677  clear
  678  docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network --volume mysql-database-volume:/var/lib/mysql  mysql:5.7
  679  history
  680  clear
  681  docker container ls
  682  docker stop 4c,4e
  683  docker stop 4c 4e
  684  clear
  685  ls
  686  pwd
  687  cd ../04-spring-boot-react-full-stack-h2/restful-web-services/
  688  ls
  689  mvn clean package
  690  pwd
  691  docker run -p 8080:8080 in28min/rest-api-full-stack:0.0.1-SNAPSHOT
  692  docker build .
  693  docker build .
  694  docker build .
  695  docker build .
  696  clear
  697  docker tag 3f4765872126 in28min/rest-api-full-stack:2stagebuild
  698  docker run -p 8080:8080 in28min/rest-api-full-stack:2stagebuild
  699  history

   462  mvn clean package
  463  pwd
  464  docker run -p 8080:8080 in28min/rest-api-full-stack:0.0.1-SNAPSHOT
  465  docker build .
  466  docker build .
  467  docker build .
  468  docker build .
  469  clear
  470  docker tag 3f4765872126 in28min/rest-api-full-stack:2stagebuild
  471  docker run -p 8080:8080 in28min/rest-api-full-stack:2stagebuild
  472  history
  473  cd ../04-spring-boot-react-full-stack-h2/frontend/todo-app/
  474  npm install
  475  npm start
  476  npm run build
  477  pwd
  478  ls
  479  clear
  480  docker build .
  481  docker build . -t in28min/todo-front-end:0.0.1-SNAPSHOT
  482  docker build . -t in28min/todo-front-end:0.0.1-SNAPSHOT
  483  docker build . -t in28min/todo-front-end:0.0.1-SNAPSHOT
  484  docker run -p 4200:80 in28min/todo-front-end:0.0.1-SNAPSHOT
  485  history
  486  ls
  487  cd ..
  488  ls
  489  take-step-backup.sh 01-startingpoint-1stage-api-2stage-frontend
  490  open .
  491  clear
  492  pwd
  493  take-step-backup.sh 02-2-stage-api-2-stage-frontend
  494  cd restful-web-services/
  495  ls
  496  clear
  497  pwd
  498  take-step-backup.sh 01-web-app-with-spotify-dockerfile-maven-plugin
  499  cd ..
  500  pwd
  501  docker network create currency-network
  502  docker run -p 8000:8000 --network=currency-network --name=currency-exchange-service in28min/currency-exchange-service:0.0.1-SNAPSHOT
  503  docker run -p 8000:8000 --network=currency-network --name=currency-exchange-service -d in28min/currency-exchange-service:0.0.1-SNAPSHOT
  504  docker container rm 3a0
  505  docker run -p 8000:8000 --network=currency-network --name=currency-exchange-service -d in28min/currency-exchange-service:0.0.1-SNAPSHOT
  506  clear
  507  docker run -p 8100:8100 --network=currency-network --name=currency-conversion-service ---env CURRENCY_EXCHANGE_URI=http://currency-exchange-service:8000 -d in28min/currency-conversion-service:0.0.1-SNAPSHOT
  508  docker run -p 8100:8100 --network=currency-network --name=currency-conversion-service --env CURRENCY_EXCHANGE_URI=http://currency-exchange-service:8000 -d in28min/currency-conversion-service:0.0.1-SNAPSHOT
  509  docker container logs -f 5fa
  510  docker container ls
  511  history
  512  clear
  513  docker container ls
  514  docker container prune -a
  515  docker container prune
  516  clear
  517  docker container ls
  518  docker container stop 5f f0
  519  docker container rm 5f f0
  520  docker container prune
  521  clear
  522  docker-compose up
  523  docker-compose up
  524  docker-compose -d up
  525  docker-compose up -d
  526  docker-compose scale currency-conversion-service 2
  527  docker-compose scale currency-conversion-service=2
  528  docker-compose up -d
  529  docker-compose logs
  530  docker-compose logs -f
  531  docker-compose scale currency-conversion-service=2
  532  docker-compose scale currency-exchange-service=2
  533  docker-compose logs -f
  534  docker-compose update
  535  docker-compose up -d
  536  docker-compose logs -f
  537  docker-compose up -d
  538  docker-compose status
  539  docker compose events
  540  docker-compose events
  541  docker-compose logs
  542  docker-compose up -d
  543  docker-compose logs -f
  544  docker-compose up -d
  545  docker-compose up
  546  docker-compose up
  547  clear
  548  docker-compose up -d
  549  docker-compose down
  550  clear
  551  docker-compose up -d
  552  docker-compose logs -f
  553  docker-compose scale currency-exchange-service=2
  554  docker-compose scale currency-exchange-service=2
  555  docker-compose logs
  556  docker-compose logs -f
  557  clear
  558  docker-compose up

499  docker --version
  500  docker run in28min/todo-rest-api-h2:1.0.0.RELEASE
  501  docker run -p 8080:8080 in28min/todo-rest-api-h2:1.0.0.RELEASE
  502  docker run in28min/todo-rest-api-h2:1.0.0.RELEASE
  503  clear
  504  docker run -p 5000:5000 in28min/todo-rest-api-h2:1.0.0.RELEASE
  505  docker image ls
  506  docker image rm in28min/todo-rest-api-h2 
  507  docker image rm in28min/todo-rest-api-h2:1.0.0.RELEASE 
  508  docker system prun
  509  docker system prune -a
  510  clear
  511  docker --version
  512  docker run in28min/todo-rest-api-h2:1.0.0.RELEASE
  513  clear
  514  docker run -p 5000:5000 in28min/todo-rest-api-h2:1.0.0.RELEASE
  515  clear
  516  docker run -p 5000:5000 -d in28min/todo-rest-api-h2:1.0.0.RELEASE
  517  docker logs c9b5ee895d644a4a3ba5b66c9accfed04369da4da725fc26e541987325ee7578
  518  docker logs -f c9b5ee895d644a4a3ba5b66c9accfed04369da4da725fc26e541987325ee7578
  519  clear
  520  docker container ls
  521  docker run -p 5001:5000 -d in28min/todo-rest-api-h2:1.0.0.RELEASE
  522  docker logs -f 38155
  523  docker container ls
  524* 
  525  docker images
  526  docker container ls -a
  527  docker container stop 38155
  528  docker container stop c9b5
  529  docker container ls -a
  530  clear
  531  docker container ls -a
  532  docker images
  533  docker run -p 5001:5000 -d in28min/todo-rest-api-h2:1.0.0.RELEASE
  534  docker logs -f ddbb
  535  clear
  536  docker images
  537  docker run -p 5001:5000 in28min/todo-rest-api-h2:1.0.0.RELEASE
  538  docker container stop 8080
  539  docker containers
  540  docker container ls
  541  docker container stop ddbb
  542  clear
  543  docker images
  544  docker run -p 5000:5000 in28min/todo-rest-api-h2:1.0.0.RELEASE
  545  clear
  546  docker run -p 5000:5000 in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
  547  clear
  548  docker search mysql
  549  docker images
  550  docker tag in28min/todo-rest-api-h2 -t tests
  551  docker tag in28min/todo-rest-api-h2:1.0.0.RELEASE latest
  552  docker images
  553  docker tag remove latest:latest
  554  docker rmi latest:latest
  555  clear
  556  docker images
  557  docker tag in28min/todo-rest-api-h2:1.0.0.RELEASE in28min/todo-rest-api-h2:latest
  558  docker images
  559  docker pull mysql
  560  docker images
  561  docker search mysql
  562  clear
  563  docker images
  564  docker image history f8049a029560
  565  docker image inspect f8049a029560
  566  clear
  567  docker imags
  568  docker images
  569  docker image remove b8fd9553f1f0
  570  docker images
  571  clear
  572  docker images
  573  docker image ls --format=`{{json .}}`
  574  docker image ls --format='{{json .}}'
  575  clear
  576  docker image ls --format='{{json .}}'
  577  clear
  578  docker imags
  579  docker images
  580  clear
  581  docker images
  582  clear
  583  docker container run -p 5000:5000 -d in28min/todo-rest-api-h2:1.0.0.RELEASE
  584  docker container pause 6478
  585  docker logs -f 6478
  586  docker container unpause 6478
  587  docker container inspect 6478
  588  clear
  589  docker container ls -a
  590  docker container prune
  591  docker container ls -a
  592  clear
  593  docker container ls
  594  docker container stop 6478c284a0da
  595  docker container logs 6478c284a0da
  596  clear
  597  docker run -p 5000:5000 in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
  598  clear
  599  docker run -p 5000:5000 -d in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
  600  docker logs 1b1
  601  docker logs 1b1
  602  clear
  603  docker container ls
  604  docker logs -f 1b155024408b
  605  clear
  606  docker container ls
  607  docker container logs -f 1b1
  608  clear
  609  docker run -p 5000:5000 -d in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
  610  docker logs -f 9b8
  611  clear
  612  docker run -p 5000:5000 -d --restart=always in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
  613  docker container ls 
  614  docker container ls
  615  docker container ls
  616  docker container ls
  617  docker container ls
  618  docker container ls -a
  619  docker container ls -a
  620  clear
  621  docker container ls -a
  622  docker container ls
  623  docker container stop cc85
  624  docker container prune
  625  clear
  626  docker container ls
  627  docker container prune
  628  docker container ls -a
  629  docker run -p 5000:5000 -d --restart=always in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
  630  docker container stop 501
  631  docker container ls -a
  632  docker container ls
  633  docker container stop 501
  634  docker container prune
  635  docker container ls
  636  clear
  637  docker events
  638  docker run -p 5000:5000 -d in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
  639  docker top
  640  docker top c710
  641  clear
  642  docker stats
  643  clear
  644  docker container ls
  645  docker container stop c710
  646  docker run -p 5000:5000 -d in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
  647  docker run -p 5001:5000 -m 512m --cpu-quota 5000  -d in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
  648  docker container logs 3fb
  649  docker container logs -f 3fb
  650  docker container stop 3fb
  651  docker run -p 5001:5000 -m 512m --cpu-quota 50000 -d in28min/todo-rest-api-h2:0.0.1-SNAPSHOT
  652  docker container logs -f 57f
  653  clear
  654  docker system df
  655  docker container prune
  656  docker image prune
  657  clear
  658  docker images
  659  docker image prune -a
  660  clear
  661  docker images
  662  docker pull in28min/todo-rest-api-h2:1.0.0.RELEASE
  663  clear
  664  docker container prune
  665  docker container ls
  666  clear
  667  docker container prune
  668  docker container ls -a
  669  docker container stop 57f a6d
  670  docker container ls -a
  671  docker container prune
  672  docker container ls -a
  673  docker images
  674  clear
  675  docker image prune
  676  docker images
  677  docker image prune
  678  clear
  679  history

    499  docker container ls
  500  docker container stop 1b1
  501  docker container kill 9b8
  502  docker container kill cc8
  503  docker container ls
  504  clear
  505  docker events
  506  docker system df
  507  clear
  508  docker events
  509  clear
  510  docker top
  511  docker container ls
  512  docker top a6d6cd317b4b
  513  docker stats
  514  history

  Deleted Networks:
web-application-mysql-network
03-todo-web-application-mysql_todo-web-application-network
currency-network
05-microservices_currency-compose-network
```