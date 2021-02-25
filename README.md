# spring-boot-docker-mysql
Demo Spring Boot application running inside docker container linked with MySQL container.

## How ro run spring with localhot envenironment

1 - assume that you already installed mysql in your pc   
   - db name : demo
   - user : root
   - password : root 

2 - Prepare JDK 11 and Maven

3 - Run build using Maven

~~~
mvn clean spring-boot:run
~~~

## How to run it with Docker

Assume you already have Docker installed. See https://docs.docker.com/installation/.

Start docker as damon with local environment : sudo dockerd -H unix:///var/run/docker.sock -H tcp://0.0.0.0:2375

First, clone the project and build locally:

~~~
git clone https://github.com/pseudojo/spring-boot-mysql-docker.git

cd spring-boot-mysql-docker

mvn clean package docker:build
~~~

## To push the image you just built to the registry, specify the pushImage flag.

~~~
mvn clean package docker:build -DpushImage
~~~

## How to run docker application with localhost database

~~~

docker-compose up -d

~~~

### Run MySQL 5.7 in Docker container (without docker-compose):

Run mysql container:

~~~
docker run --name demo-mysql -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=demo -e DATABASE_USER=demo_user -e DATABASE_PASSWORD=demo_pass -p  3306:3306 -d mysql:5.7
~~~

Check the log to make sure the server is running OK:

~~~
docker logs demo-mysql
~~~

Run demo application in Docker container and link to demo-mysql:

~~~
docker run -p 8080:8080 --name web-app --link demo-mysql:mysql -d sopheamak/springboot_docker_mysql

docker run -p 8080:8080 --name web-app -d sopheamak/springboot_docker_mysql
~~~

You can check the log by
~~~
docker logs demo-app
~~~

