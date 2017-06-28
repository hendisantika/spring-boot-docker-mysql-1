# spring-boot-docker-mysql
Demo Spring Boot application running inside docker container linked with MySQL container.

See my [blog post about it](https://github.com/sophea/spring-boot-docker-mysql/wiki/home).

## How to run it with Docker
Assume you already have Docker installed. See https://docs.docker.com/installation/.

First, clone the project and build locally:

~~~
git clone https://github.com/sophea/spring-boot-docker-mysql.git
cd spring-boot-docker-mysql

mvn clean package docker:build
~~~

Run MySQL 5.7 in Docker container:

~~~
docker run --name demo-mysql -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=demo -e MYSQL_USER=demo_user -e MYSQL_PASSWORD=demo_pass -p  3306:3306 -d mysql:5.7
~~~

Check the log to make sure the server is running OK:
~~~
docker logs demo-mysql
~~~

Run demo application in Docker container and link to demo-mysql:

~~~
docker run -p 8080:8080 --name web-app --link demo-mysql:mysql -d sopheamak/springboot_docker_mysql

~~~

You can check the log by
~~~
docker logs demo-app
~~~



## To push the image you just built to the registry, specify the pushImage flag.

mvn clean package docker:build -DpushImage


## check docker logs

docker logs dockerwar


more about docker plugin with maven : https://github.com/spotify/docker-maven-plugin#authentication



## Docker-compose

To run this you need to install docker-compose first

>>cd target/docker

>>docker-compose up -d