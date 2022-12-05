# Spring Boot :whale: Docker

## About Spring Boot and this example

[Spring Boot](https://spring.io/projects/spring-boot) allows you to create stand-alone Spring applications by embedding an application server.

It provides production-ready features like metrics or health-checks and simplifies the build configuration overall.

In this example you can check how to dockerize a Spring Boot application so you can run your container anywhere.

## Technical requirements

You are going to need only 2 things

- A Spring Boot project. If you need some help at setting it up you can check how  [in this example](https://github.com/codewithhades/spring-boot-basic-setup)
- [Docker](https://www.docker.com), so you can dockerize the application

## How to build the docker image

- Firstly you need to package your application into a JAR that will be generated withing the target folder
    ````bash
    mvn clean package
    ````

- The next thing is to create a [Dockerfile](docker/Dockerfile) that is based on a JDK that matches the one used by your project. It should copy the previously generated JAR and run the java command as entrypoint
    ````Dockerfile
    FROM openjdk:19-jdk-slim
    COPY /target/spring-boot-docker.jar /app.jar
    ENTRYPOINT ["java","-jar","/app.jar"]
    ````

- With the JAR generated and your [Dockerfile](docker/Dockerfile) you can now build your image by executing
    ````bash
    docker build -t spring-boot-docker -f docker/Dockerfile .
    ````
- You can make sure that the image was successfully created by listing all the images
    ````bash
    docker images
    
    REPOSITORY           TAG       IMAGE ID       CREATED        SIZE
    spring-boot-docker   latest    6fcca5332653   24 hours ago   445MB
    ````

## How to run the docker image

You can now run your image by executing the following command (making sure that you link the 8080 ports to allow http connections)
````bash
docker run -p 8080:8080 spring-boot-docker
````
After executing the command you should be able to see the Spring Boot starting logs and access the application actuator by browsing [localhost:8080/app/actuator/health](http://localhost:8080/app/actuator/health)

## And before you go...

:pray: I hope you find this example useful and if you want to support me in my mission to help our fellow Java developers please consider starring and sponsoring this space!

:coffee: May Java be with you!