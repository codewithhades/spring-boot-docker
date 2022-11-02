# Spring Boot :whale: Docker

## About Spring Boot and this example

[Spring Boot](https://spring.io/projects/spring-boot) allows you to create stand-alone Spring applications by embedding an application server.

It provides production-ready features like metrics or health-checks and simplifies the build configuration overall.

In this example you can check how to dockerize a Spring Boot application so you can run your container anywhere.

## Technical requirements

You are going to need only 2 things

- [Docker](https://www.docker.com) - _in order to dockerize our application_
- A running Spring Boot application - _like this [example with actuator](https://github.com/codewithhades/spring-boot-actuator)_

## How to build the docker image

````bash
mvn clean package
docker build -t spring-boot-docker -f docker/Dockerfile .
docker images
````

## How to run the docker image

````bash
docker run -p 8080:8080 spring-boot-docker
````