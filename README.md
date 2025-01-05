# spring-boot-dumps

## Why we need Spring Framework?

### Servlet and Servlet containers
- Provides foundation for building web applications.
- Servlet is a Java class, which handles client request, process it and returns the response.
- Each Servlet handles get, post, put, delete kinda requests, and provides responses.
- Servlet Containers are the ones that manages the servlets.
- Web.xml this is where we write details of each mapping and servlets, provinding a type of filtering.
![Alt text](images/servlet.png)


### Spring MVC and advantages over servlet
- Solves challenges which exists with servlets.

1. Removal of Web.xml 
- as it becomes too big to be handled when scaled.
- Spring introduces Annotations based configurations.

2. Inversion of Control
- provides more flexible way to manage Object dependencies and its lifecycle via Dependency Injection.

3. Easier Unit Testing  
- Earlier the object creation depends on servlet, mocking was difficult making UT hard.
- With DI it becomes very easy.

4. Easy to Manage RESTful APIs
- Spring MVC provides an organised approach to handle the requests and its easy to build RESTful APIs.

Refer to the flow below for spring
![Alt text](images/spring.png)

### Spring Boot and advantages over Spring MVC
Spring boot solves challenges which exists in Spring MVC. It provides a quick way to create a production ready application based on spring framework.

1. Dependency Management: No need for adding different dependencies seperately and their compatible versions.
2. Auto Configuration: No need for seperately configuring "DispatcherServlet", "AppConfig","EnableWebMvc","ComponentScan".Spring boot adds them internally.
3. Embedded Server: In Spring boot, Servlet container is already embedded, we dont need to deploy the WAR files. Just run the application.

## Setup Spring Boot Application
- Go to start.spring.io
- JAR - Java Archive - for Java standalone application, currently used in microservice world
- WAR - Web Archieve - when we need HTML, CSS, JS and other files
- Add Spring web as dependency and we can add other dependency later.
- Click on Generate and import the folder in any IDE like VSCode or IntelliJ

## Layered Architecture
Most companies prefer this kinda architecure for their applications
![Alt text](images/architecture.png)

Controller Layer: handles all the controllers. Classes which host endpoints. having @Controller  / @RestController
Service Layer: handles bussiness logic.
Repository Layer: handles interactions with the db

DTO: Data Transfer Objects -  to transfer data amoung layers.
Utility: represents common methods or helper methods.
Entity: @Entity aka POJOs provides direct representation of the tables in the db. helps in data insertion/extraction.
Configuration: for handling configurations. present in application.configuration files. Differs based on ENVs.


## Maven
- Its a project management tool.Helps with
    - Build generation
    - Dependency resolution
    - Documentation etc
- Maven uses POM(Project Object Model) to achieve this.
- When maven command is executed, it looks for "pom.xml" in the current directory and gets needed configurations.
- In Maven we generally need to tell What to do and it knows how to do.
- Before maven, Ant was popular but there we need to tell it what to do adn how to do.

### Project Structure for maven
![Alt Text](images/maven.png)


### POM file structure
```xml
<?xml version="1.0" encoding="UTF-8"?>

<!-- Specifies the XML Schema, and makes sure out pom file adheres to it. -->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	
    
    <!-- Used to Defile the parent project -->
    <!-- Each pom has one parent pom bydefault. -->
    <!-- Superpom is at the top of hierarchy. Used if this parent field is not specified. -->
    <parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.4.1</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>


    <!-- Uniquely identifies the project -->
	<groupId>com.example</groupId>
	<artifactId>spring-boot-dumps</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>Spring boot Dump Project</name>
	<description>Project for Spring Boot</description>
	

    <!-- Define key value pair for configurations. And later can be references anywhere -->
	<properties>
		<java.version>17</java.version>
	</properties>

    <!-- This is where maven looks for dependencies and download the artifacts(jars). -->
    <!-- bydefault present in superpom.  -->
    <repositories>
		<repository>
			<id>central</id>
			<url>https://repo1.maven.org/maven2/</url>
		</repository>
	</repositories>



	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

    <!-- defines the maven lifecycle,  -->
	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>

```


### Maven Build Lifecycle
- Maven lifecycle is divided into 7 phases and each phase has multiple goals(tasks).
- If you run any phase/goal, all the phases/goals prior to that phase/goal executes first.

![Alt Text](images/maven-lifecycle.png)

1. validate: validates the code before compiling. Maven does't restrict anything here but we can add goals. Like validating code style, formatting etc.
2. compile: converts the java code to bytecode. .class files. Puts the bytecode into target/classes.
3. test: runs the test cases of the project in src/test
4. package: package compiled code into JAR(.jar) or WAR(.war).
5. verify: check the integrity of the package. Maven does't restrict anything here but we can add goals. like PMD source code analyzer.
6. install: Installs the .jar package into local repository. typically located in (~/.m2/repository). We can change the path in /.m2/settings.xml file.
7. deploy: Installs the .jar package into remote repository. We can provide the repo url in the pom file and private repo we can put username & password in settings.xml. If we try to run deploy without providing the url we will see the error.

Note: If we want to deploy the manifest to maven central repository we can use: https://repo.maven.apache.org/maven2/. Since its public we dont need username and password.

Note: To configure remote repo:
![Alt text](images/remote-repo-config.png)
