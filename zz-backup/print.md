## Todo
- Use UNIX Containers on Windows
- play-with-docker.com
- Plugins
  - Fabric8 Plugin
  - https://stackabuse.com/dockerizing-a-spring-boot-application/
- Network Types
  - `docker network ls`
- Volumes
  - Accessing host device in container `--device=HOST_PATH:CONTAINER_PATH`
  - Persisting data using volumes. `create volume customvol` `-v customvol:/data` `docker volume inspect`
  - Share Data between Host and container `-V $(HOME)/data_share:/data`
- Pushing an Image
  - You need Registry, Repository and Tag
  - `docker image build -t web:latest . ` (If you push this, you will get an error. Because you need to specify a repository)
  - `docker image build -t in28min/web:latest .`
  - `docker image push`
  - `docker.io/in28min/spring-boot:1.0.0.SNAPSHOT`
  -   DEFAULT   REPOSITORY          TAG  
- Commands
  - `docker system prune`
  - `docker system prune -a`
  - `docker image prune`
  - `docker container prune`
  - `docker network prune`
  - `docker network ls`
  - `docker container ls`
  - `docker volume ls`
  - `docker events`
  - `docker stats`
- Create Auto Build 
  - Github & Docker Hub


### Commands

### Image

Versions 
  -  `<repository>:<tag> `
  -  tag - latest might not be latest 
  -  Single image can have multiple tags 
  -  Search for image `docker search` 
  -  Official vs Personal Images 
  -  Delete unused images (-a)
  -  docker image prune -a

docker image
- ls, rm, history, inspect, prune, --filter --format

- `docker images`
- `docker image history f8049a029560`
- `docker image history in28min/todo-rest-api-h2`
- `docker image inspect 01-hello-world-rest-api:0.0.1-SNAPSHOT`
- `docker image remove f8049a029560`
- `docker images --format "table {{.Repository}}\t{{.Tag}}\t{{.CreatedSince}}"`
- `docker container ls --format='{{json .}}'`
- `docker image ls --format='{{json .}}'`
- `docker image ls --format='{{.Containers}} {{.Tag}}'`


#### Layers 
  -  `docker image pull` shows all underlying layers - docker pull in28min/aws-currency-exchange-service-h2:0.0.1-SNAPSHOT
  -  `docker image inspect` shows layers
  -  Image layers lead to efficiencies in space and performance. Download 2 similar images and show that common layers are not downloaded.
  -  Copy files and show layers

#### Containers
Docker Containers -> run -it, -d, ls , exect -it name bash, stop, run, logs, inspect, pause, unpause
  -  Multiple containers from one image
  -  Containers can persist data -> mysql db example, creating new files 
  -  Using $ID syntax
  -  Stop and remove all containers -> docker container prune
  -  Specifying constraints `-m 512m` `-m 1G` `--memory-reservation 128m` `--cpu-quota 50000` 100%=100000
  -  Running two instances of app on different ports in a container and exposing them using a different port

```
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
```

### /01-hello-world-rest-api/Dockerfile
- `docker pull in28min/aws-currency-exchange-service-h2:0.0.1-SNAPSHOT`
- Command vs Entrypoint
- Building Images
   - Build Context - Directory containing the app - typically the directory containing Dockerfile. . is important.
   - Dockerfile - Two types of commands - 1. build layers 2. Adds Metadata
   - `docker image build -t web:latest . `
- Docker File
   - Hash(`#`) -> Comment Line
   - All non comment lines are instructions
   - `EXPOSE, WORKDIR, ENV, ENTRYPOINT` -> Add meta data.


```Dockerfile
FROM openjdk:8-jdk-alpine
VOLUME /tmp
EXPOSE 80
ADD target/*.jar app.jar
ENV JAVA_OPTS=""
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -jar /app.jar" ]
```
## Plugins

### Dockerfile Maven

- https://github.com/spotify/dockerfile-maven

```xml
      <plugin>
        <groupId>com.spotify</groupId>
        <artifactId>dockerfile-maven-plugin</artifactId>
        <version>1.4.10</version>
        <executions>
          <execution>
            <id>default</id>
            <goals>
              <goal>build</goal>
              <goal>push</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <repository>in28min/${project.name}</repository>
          <tag>${project.version}</tag>
          <skipDockerInfo>true</skipDockerInfo>
        </configuration>
      </plugin>
```
### JIB

- https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin#quickstart
- https://github.com/GoogleContainerTools/jib/blob/master/docs/faq.md
- `<useCurrentTimestamp>true</useCurrentTimestamp>` - https://github.com/GoogleContainerTools/jib/issues/413 

- mvn compile jib:build -Dimage=in28minutes/test
- mvn compile jib:dockerBuild -Dimage=in28minutes/test
- After adding configuration - mvn -X package -DskipTests


```xml
<plugin>
  <groupId>com.google.cloud.tools</groupId>
  <artifactId>jib-maven-plugin</artifactId>
  <version>1.6.1</version>
  <configuration>
    <container>
      <creationTime>USE_CURRENT_TIMESTAMP</creationTime>
    </container>
  </configuration>
  <executions>
    <execution>
      <phase>package</phase>
      <goals>
        <goal>dockerBuild</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```
```xml
<configuration>
  <from>
    <image>openjdk:alpine</image>
  </from>
  <to>
    <image>in28min/${project.name}</image>
    <tags>
      <tag>${project.version}</tag>
      <tag>latest</tag>
    </tags>
  </to>
  <container>
    <jvmFlags>
      <jvmFlag>-Xms512m</jvmFlag>
    </jvmFlags>
    <mainClass>com.in28minutes.rest.webservices.restfulwebservices.RestfulWebServicesApplication</mainClass>
    <ports>
      <port>8100</port>
    </ports>
  </container>
</configuration>
```
### Maven Dependency Plugin
```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-dependency-plugin</artifactId>
  <executions>
    <execution>
      <id>unpack</id>
      <phase>package</phase>
      <goals>
        <goal>unpack</goal>
      </goals>
      <configuration>
        <artifactItems>
          <artifactItem>
            <groupId>${project.groupId}</groupId>
            <artifactId>${project.artifactId}</artifactId>
            <version>${project.version}</version>
          </artifactItem>
        </artifactItems>
      </configuration>
    </execution>
  </executions>
</plugin>
```

---
### /02-todo-web-application-h2/Dockerfile

```Dockerfile
From tomcat:8.0.51-jre8-alpine
RUN rm -rf /usr/local/tomcat/webapps/*
COPY ./target/*.war /usr/local/tomcat/webapps/ROOT.war
CMD ["catalina.sh","run"]
```
---
### JIB
```xml
<plugin>
  <groupId>com.google.cloud.tools</groupId>
  <artifactId>jib-maven-plugin</artifactId>
  <version>1.6.1</version>
  <configuration>
    <from>
      <image>tomcat:8.5-jre8-alpine</image>
    </from>
    <container>
      <appRoot>/usr/local/tomcat/webapps/my-webapp</appRoot>
      <creationTime>USE_CURRENT_TIMESTAMP</creationTime>
    </container>
  </configuration>
  <executions>
    <execution>
      <phase>package</phase>
      <goals>
        <goal>dockerBuild</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```
---
### /03-todo-web-application-mysql/Dockerfile

NO CHANGE
---
`docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 mysql:5.7`

```
mysqlsh
\connect todos-user@localhost:3306
\sql
use todos
select * from todos;
```
---


### application.properties
```properties
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://${RDS_HOSTNAME:localhost}:${RDS_PORT:3306}/${RDS_DB_NAME:todos}
spring.datasource.username=${RDS_USERNAME:todos-user}
spring.datasource.password=${RDS_PASSWORD:dummytodos}
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL57Dialect
```

---
### docker-compose.yml

```yml
version: '3.7'
# Removed subprocess.CalledProcessError: Command '['/usr/local/bin/docker-credential-desktop', 'get']' returned non-zero exit status 1
# I had this:
# cat ~/.docker/config.json
# {"auths":{},"credsStore":"", "credsStore":"desktop","stackOrchestrator":"swarm"}
# I updated to this:
# {"auths":{},"credsStore":"","stackOrchestrator":"swarm"}
services:
  todo-web-application:
    #image: in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
    build:
      context: .
      #dockerfile: Dockerfile
    ports:
      - "8080:8080"
    restart: always
    depends_on: # Start the depends_on first
      - mysql 
    environment:
      RDS_HOSTNAME: mysql
      RDS_PORT: 3306
      RDS_DB_NAME: todos
      RDS_USERNAME: todos-user
      RDS_PASSWORD: dummytodos
    networks:
      - todo-web-application-network

  # Database Service (Mysql)
  mysql:
    image: mysql:5.7
    ports:
      - "3306:3306"
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_ROOT_PASSWORD: dummypassword 
      MYSQL_USER: todos-user
      MYSQL_PASSWORD: dummytodos
      MYSQL_DATABASE: todos
    volumes:
      - mysql-database-data:/var/lib/mysql
    networks:
      - todo-web-application-network  
  
# Volumes
volumes:
  mysql-database-data:

# Networks to be created to facilitate communication between containers
networks:
  todo-web-application-network:
```

---

### /04-spring-boot-react-full-stack-h2/docker-compose.yml

```yml
version: '3.7'
# Removed subprocess.CalledProcessError: Command '['/usr/local/bin/docker-credential-desktop', 'get']' returned non-zero exit status 1
# I had this:
# cat ~/.docker/config.json
# {"auths":{},"credsStore":"", "credsStore":"desktop","stackOrchestrator":"swarm"}
# I updated to this:
# {"auths":{},"credsStore":"","stackOrchestrator":"swarm"}
services:
  todo-frontend:
    #image: in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
    build:
      context: frontend/todo-app
      #context: .
      #dockerfile: Dockerfile
    ports:
      - "4000:80"
    restart: always
    depends_on: # Start the depends_on first
      - todo-api 
    #environment:
      #BACKEND_API_BASE_URL: http://localhost:8080
    networks:
      - fullstack-application-network

  todo-api:
    #image: in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
    build:
      context: restful-web-services
      #context: .
      #dockerfile: Dockerfile
    ports:
      - "8080:8080"
    restart: always
    #depends_on: # Start the depends_on first
      #- todo-api 
    networks:
      - fullstack-application-network
  
# Networks to be created to facilitate communication between containers
networks:
  fullstack-application-network:
```
---

### /frontend/todo-app/Dockerfile

- Multi Stage Builds -> Page 149 to 155

```Dockerfile
## Stage 1 - Lets build the "deployable package"
FROM node:7.10 as frontend-build
WORKDIR /fullstack/frontend

# Step 1 - Download all package dependencies first.
# We will redownload dependencies only when packages change.
COPY package.json package-lock.json ./
RUN npm install

# Step 2 - Copy all source and run build
COPY . ./
RUN npm run build

## Stage 2 - Let's build a minimal image with the "deployable package"
FROM nginx:1.12-alpine
COPY --from=frontend-build /fullstack/frontend/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```
---

### restful-web-services/Dockerfile

```Dockerfile
## Stage 1 - Lets build the "deployable package"
FROM maven:3.6.1-jdk-8-alpine as backend-build
WORKDIR /fullstack/backend

# Step 1 - Copy pom.xml and download project dependencies
# Dividing copy into two steps to ensure that we download dependencies 
# only when pom.xml changes
COPY pom.xml .
# dependency:go-offline - Goal that resolves all project dependencies, 
# including plugins and reports and their dependencies. -B -> Batch mode
RUN mvn dependency:go-offline -B

# Step 2 - Copy source and build "deployable package"
COPY src src
RUN mvn install -DskipTests

# Unzip
RUN mkdir -p target/dependency && (cd target/dependency; jar -xf ../*.jar)

## Stage 2 - Let's build a minimal image with the "deployable package"
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG DEPENDENCY=/fullstack/backend/target/dependency
COPY --from=backend-build ${DEPENDENCY}/BOOT-INF/lib /app/lib
COPY --from=backend-build ${DEPENDENCY}/META-INF /app/META-INF
COPY --from=backend-build ${DEPENDENCY}/BOOT-INF/classes /app
ENTRYPOINT ["java","-cp","app:app/lib/*","com.in28minutes.rest.webservices.restfulwebservices.RestfulWebServicesApplication"]
```
---

## /05-simple-microservices/currency-conversion-service

- Basic - `docker container run --publish 8000:8000 in28min/currency-exchange-service:0.0.1-SNAPSHOT`
- Custom Network 
  - `docker network create currency-network`
  - `docker run --publish 8000:8000 --network currency-network --name=currency-exchange-service in28min/currency-exchange-service:0.0.1-SNAPSHOT`
  - `docker run --publish 8100:8100 --network currency-network --env CURRENCY_EXCHANGE_URI=http://currency-exchange-service:8000 in28min/currency-conversion-service:0.0.1-SNAPSHOT`
  - `docker run -p 8000:8000 --network currency-network --name currency-exchange-service c047b15426b8`
  - `docker run -p 8000:8000 --network currency-network --name currency-exchange-service c047b15426b8`
  - `docker run -p 8100:8100 --network currency-network -e CURRENCY_EXCHANGE_URI=http://currency-exchange-service:8000 f1`

### /Dockerfile

```Dockerfile
EXPOSE 8100
```
---

### pom.xml
- Standard - Spotify Maven Plugin
```xml
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>

<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-zipkin</artifactId>
</dependency>

<dependency>
	<groupId>org.springframework.amqp</groupId>
	<artifactId>spring-rabbit</artifactId>
</dependency>
```
---
### CurrencyConversionServiceApplication.java

```java
@EnableDiscoveryClient
public class CurrencyConversionServiceApplication {

```
---

### CurrencyExchangeServiceProxy.java

```java
@FeignClient(name = "currency-exchange-service", url="${CURRENCY_EXCHANGE_URI:http://localhost:8000}")
@FeignClient(name="netflix-zuul-api-gateway-server")
public interface CurrencyExchangeServiceProxy {

	@GetMapping("/currency-exchange/from/{from}/to/{to}")
	@GetMapping("/currency-exchange-service/currency-exchange/from/{from}/to/{to}")
	public CurrencyConversionBean retrieveExchangeValue(@PathVariable("from") String from,
			@PathVariable("to") String to);
}
```
---
---

### /application.properties

```properties
# Eureka
#eureka.client.service-url.default-zone=http://localhost:8761/eureka
eureka.client.service-url.defaultZone=http://naming-server:8761/eureka/

# RabbitMQ
spring.rabbitmq.host=rabbitmq
spring.sleuth.sampler.probability=1.0

```
---

---

### /05-simple-microservices/currency-exchange-service/Dockerfile

```Dockerfile
EXPOSE 8000
```
---

### /pom.xml
- Standard - Spotify Maven Plugin
```xml
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-zipkin</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.amqp</groupId>
			<artifactId>spring-rabbit</artifactId>
		</dependency>
```
---

### CurrencyExchangeServiceApplicationH2.java

```java

@SpringBootApplication
@EnableDiscoveryClient
public class CurrencyExchangeServiceApplicationH2 {
```
---

### /application.properties

```properties
# Eureka
#eureka.client.service-url.default-zone=http://localhost:8761/eureka
eureka.client.service-url.defaultZone=http://naming-server:8761/eureka/

# RabbitMQ
spring.rabbitmq.host=rabbitmq
spring.sleuth.sampler.probability=1.0

```
---

### /05-simple-microservices/docker-compose-starting.yml

Docker Compose 
- `docker-compose --version` 
- default - `docker-compose.yaml` or `-f custom-name.yaml`
- `docker-compose up -d`


```yml
version: '3.7'
# Removed subprocess.CalledProcessError: Command '['/usr/local/bin/docker-credential-desktop', 'get']' returned non-zero exit status 1
# I had this:
# cat ~/.docker/config.json
# {"auths":{},"credsStore":"", "credsStore":"desktop","stackOrchestrator":"swarm"}
# I updated to this:
# {"auths":{},"credsStore":"","stackOrchestrator":"swarm"}
services:
  currency-exchange-service:
    #image: in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
    build:
      context: currency-exchange-service
      #context: .
      #dockerfile: Dockerfile
    ports:
      - "8000:8000"
    restart: always
    #depends_on: # Start the depends_on first
      #- todo-api 
    environment:
      BACKEND_API_BASE_URL: http://localhost:8080
      RDS_PORT: 3306
    networks:
      - currency-network

  currency-conversion-service:
    #image: in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
    build:
      context: currency-conversion-service
      #context: .
      #dockerfile: Dockerfile
    ports:
      - "8100:8100"
    restart: always
    depends_on: # Start the depends_on first
      - currency-exchange-service
    environment:
      CURRENCY_EXCHANGE_URI: http://currency-exchange-service:8000
    networks:
      - currency-network
  
# Networks to be created to facilitate communication between containers
networks:
  currency-network:
```
---

### /05-simple-microservices/docker-compose.yml

```yml
version: '3.7'
# Removed subprocess.CalledProcessError: Command '['/usr/local/bin/docker-credential-desktop', 'get']' returned non-zero exit status 1
# I had this:
# cat ~/.docker/config.json
# {"auths":{},"credsStore":"", "credsStore":"desktop","stackOrchestrator":"swarm"}
# I updated to this:
# {"auths":{},"credsStore":"","stackOrchestrator":"swarm"}
services:

  rabbitmq:
    container_name: rabbitmq
    image: rabbitmq:3.5.3-management
    ports:
      - "5672:5672"
      - "15672:15672"
    networks:
      - currency-microservices-network

  naming-server:
    build: netflix-eureka-naming-server
    container_name: naming-server
    ports:
      - "8761:8761"
      - "28787:8787"
    networks:
      - currency-microservices-network

  zipkin-server:
    image: openzipkin/zipkin
    container_name: zipkin
    environment:
      - STORAGE_TYPE=mem
      # Uncomment to enable debug logging
      # - JAVA_OPTS=-Dlogging.level.zipkin=DEBUG
    depends_on: # Start the depends_on first
      - rabbitmq
    environment:
      - RABBIT_URI=amqp://guest:guest@rabbitmq:5672
    ports:
      - 9411:9411
    networks:
      - currency-microservices-network

  currency-exchange-service:
    image: in28min/currency-exchange-service:0.0.1-SNAPSHOT
    container_name: currency-exchange-service
    #build:
      #context: ../05-simple-microservices/currency-exchange-service
      #context: .
      #dockerfile: Dockerfile
    ports:
      - "8000:8000"
    restart: always
    depends_on: # Start the depends_on first
      - rabbitmq
      - zipkin-server
      - naming-server
      - zuul-api-gateway
    environment:
      - RABBIT_URI=amqp://guest:guest@rabbitmq:5672
    networks:
      - currency-microservices-network

  currency-conversion-service:
    image: in28min/currency-conversion-service:0.0.1-SNAPSHOT
    container_name: currency-conversion-service
    #build:
      #context: ../05-simple-microservices/currency-conversion-service
      #context: .
      #dockerfile: Dockerfile
    ports:
      - "8100:8100"
    restart: always
    depends_on: # Start the depends_on first
      - rabbitmq
      - zipkin-server
      - currency-exchange-service
      - naming-server
      - zuul-api-gateway
    environment:
      - CURRENCY_EXCHANGE_URI=http://currency-exchange-service:8000
      - RABBIT_URI=amqp://guest:guest@rabbitmq:5672
    networks:
      - currency-microservices-network

  zuul-api-gateway:
    image: in28min/netflix-zuul-api-gateway-server:0.0.1-SNAPSHOT
    container_name: zuul-api-gateway
    #build:
      #context: ../05-simple-microservices/currency-conversion-service
      #context: .
      #dockerfile: Dockerfile
    ports:
      - "8765:8765"
    restart: always
    depends_on: # Start the depends_on first
      - rabbitmq
      - zipkin-server
      - naming-server
    environment:
      - RABBIT_URI=amqp://guest:guest@rabbitmq:5672
    networks:
      - currency-microservices-network
  
# Networks to be created to facilitate communication between containers
networks:
  currency-microservices-network:
```
---

### /05-simple-microservices/netflix-eureka-naming-server

```Dockerfile
EXPOSE 8761
```
---

### pom.xml
- Standard - Spotify Maven Plugin
```xml
<dependency>
	<groupId>org.springframework.cloud</groupId>
	<artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```
---

### NetflixEurekaNamingServerApplication.java

```java
@SpringBootApplication
@EnableEurekaServer
public class NetflixEurekaNamingServerApplication {
```
---

### application.properties

```properties
spring.application.name=netflix-eureka-naming-server
server.port=8761

eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

---

### /05-simple-microservices/netflix-zuul-api-gateway-server/Dockerfile

```Dockerfile
EXPOSE 8765
```
---

### pom.xml
- Standard - Spotify Maven Plugin
```xml
<artifactId>spring-cloud-starter-netflix-zuul</artifactId>
<artifactId>spring-cloud-starter-sleuth</artifactId>
<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
<artifactId>spring-cloud-starter-zipkin</artifactId>
<artifactId>spring-rabbit</artifactId>
```
---

### NetflixZuulApiGatewayServerApplication.java

```java
@EnableZuulProxy
@EnableDiscoveryClient
@SpringBootApplication
public class NetflixZuulApiGatewayServerApplication {
	
	@Bean
	public Sampler defaultSampler(){
		return Sampler.ALWAYS_SAMPLE;
	}
}
```
---

### ZuulLoggingFilter.java

```java
@Component
public class ZuulLoggingFilter extends ZuulFilter{

	private Logger logger = LoggerFactory.getLogger(this.getClass());

	@Override
	public boolean shouldFilter() {
		return true;
	}

	@Override
	public Object run() {
		HttpServletRequest request = 
				RequestContext.getCurrentContext().getRequest();
		logger.info("request -> {} request uri -> {}", 
				request, request.getRequestURI());
		return null;
	}

	@Override
	public String filterType() {
		return "pre";
	}

	@Override
	public int filterOrder() {
		return 1;
	}
}
```
---

### application.properties

```properties
spring.application.name=netflix-zuul-api-gateway-server
server.port=8765

eureka.client.service-url.defaultZone=http://naming-server:8761/eureka/

spring.rabbitmq.host=rabbitmq
spring.sleuth.sampler.probability=1.0
```
---