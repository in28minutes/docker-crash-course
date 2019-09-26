# Todo Web Application using Spring Boot and MySQL as Database

Run com.in28minutes.springboot.web.SpringBootFirstWebApplication as a Java Application.

Runs on default port of Spring Boot - 8080

Application uses h2 database to run the tests.

## Can be run as a Jar or a WAR

`mvn clean install` generate a war which can deployed to your favorite web server.

We will deploy to Cloud as a WAR

## Web Application

- http://localhost:8080/login with in28minutes/dummy as credentials
- You can add, delete and update your todos
- Spring Security is used to secure the application
- `com.in28minutes.springboot.web.security.SecurityConfiguration` contains the in memory security credential configuration.


## Changes from H2 Application

#### pom.xml

```
<dependency>
	<groupId>com.h2database</groupId>
	<artifactId>h2</artifactId>
	<scope>test</scope>
</dependency>
<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
</dependency>
```

#### src/main/resources/application.properties

```
#spring.h2.console.enabled=true
#spring.h2.console.settings.web-allow-others=true

spring.jpa.hibernate.ddl-auto=update
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL55Dialect
spring.datasource.url=jdbc:mysql://localhost:3306/todos
spring.datasource.username=todos-user
spring.datasource.password=dummytodos
```

#### src/test/resources/application.properties

```
spring.jpa.hibernate.ddl-auto=create-drop
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.url=jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1
spring.datasource.username=sa
spring.datasource.password=sa
```

#### public class Todo

```
@Size(min=10, message="Enter at least 10 Characters...")
@Column(name="description")
private String desc;
```
## My SQL

### Launching MySQL using Docker

```
docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 mysql:5.7
```

Using Custom Network

```
docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network mysql:5.7
```

Using a Volume

```
docker run --detach --env MYSQL_ROOT_PASSWORD=dummypassword --env MYSQL_USER=todos-user --env MYSQL_PASSWORD=dummytodos --env MYSQL_DATABASE=todos --name mysql --publish 3306:3306 --network=web-application-mysql-network --volume mysql-database-volume:/var/lib/mysql  mysql:5.7
```

### Launching Web App using Docker

Using Link

```
docker container run -p 8080:8080 --link=mysql -e RDS_HOSTNAME=mysql  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
```

Using Custom Network

```
docker container run -p 8080:8080 --network=web-application-mysql-network -e RDS_HOSTNAME=mysql  in28min/todo-web-application-mysql:0.0.1-SNAPSHOT
```

### Playing with custom networks

```
docker network ls
docker network create web-application-mysql-network
docker inspect web-application-mysql-network
```

### Host Networking in Docker for Mac

- https://docs.docker.com/network/host/

>The host networking driver only works on Linux hosts, and is not supported on Docker Desktop for Mac, Docker Desktop for Windows, or Docker EE for Windows Server.

### My SQL Shell Client

- https://dev.mysql.com/downloads/shell/

- Install on mac using `brew install caskroom/cask/mysql-shell`.


```
Rangas-MacBook-Air:projects rangakaranam$ mysqlsh
MySQL Shell 8.0.15
Copyright (c) 2016, 2019, Oracle and/or its affiliates. All rights reserved.
Oracle is a registered trademark of Oracle Corporation and/or its affiliates.
Other names may be trademarks of their respective owners.

Type '\help' or '\?' for help; '\quit' to exit.

MySQL  JS > \connect todos-user@localhost:3306
Creating a session to 'todos-user@localhost:3306'
Please provide the password for 'todos-user@localhost:3306': 
Save password for 'todos-user@localhost:3306'? [Y]es/[N]o/Ne[v]er (default No): v
Fetching schema names for autocompletion... Press ^C to stop.
Your MySQL connection id is 37
Server version: 5.7.26 MySQL Community Server (GPL)
No default schema selected; type \use <schema> to set one.

 MySQL  localhost:3306 ssl  JS > \sql
Switching to SQL mode... Commands end with ;

 MySQL  localhost:3306 ssl  SQL > use todos
Default schema set to `todos`.
Fetching table and column names from `todos` for auto-completion... Press ^C to stop.

 MySQL  localhost:3306 ssl  todos  SQL > select * from todo ;
+----+--------------+---------+----------------------------+-------------+
| id | description  | is_done | target_date                | user        |
+----+--------------+---------+----------------------------+-------------+
|  1 | Default Desc | 0       | 2019-06-26 18:30:00.000000 | in28minutes |
+----+--------------+---------+----------------------------+-------------+
1 row in set (0.0032 sec)

```

### Create Todo Table for Production

```
create table hibernate_sequence (next_val bigint) engine=InnoDB
insert into hibernate_sequence values ( 1 )
create table todo (id integer not null, description varchar(255), is_done bit not null, target_date datetime(6), user varchar(255), primary key (id)) engine=InnoDB
```