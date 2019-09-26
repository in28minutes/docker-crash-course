# Todo Web Application using Spring Boot and H2 In memory database

Run com.in28minutes.springboot.web.SpringBootFirstWebApplication as a Java Application.

Runs on default port of Spring Boot - 8080 

## Can be run as a Jar or a WAR

`mvn clean install` generate a war which can deployed to your favorite web server.

We will deploy to Docker as a WAR

## Web Application

- http://localhost:8080/login with in28minutes/dummy as credentials
- You can add, delete and update your todos
- Spring Security is used to secure the application
- `com.in28minutes.springboot.web.security.SecurityConfiguration` contains the in memory security credential configuration.

## H2 Console

- http://localhost:8080/h2-console
- Use `jdbc:h2:mem:testdb` as JDBC URL 


## Plugins

### Dockerfile Maven

- https://github.com/spotify/dockerfile-maven

```
	<plugin>
		<groupId>com.spotify</groupId>
		<artifactId>dockerfile-maven-plugin</artifactId>
		<version>1.4.10</version>
		<executions>
			<execution>
				<id>default</id>
				<goals>
					<goal>build</goal>
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

```
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