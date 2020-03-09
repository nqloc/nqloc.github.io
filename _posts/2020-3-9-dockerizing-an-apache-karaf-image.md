---
layout: post
title: Dockerizing an Apache Karaf image
category: Karaf, OSGI, Apache Karaf, Docker
tags: [Karaf, OSGI, Apache Karaf, Docker]
active: true
---
## Download karaf from <http://karaf.apache.org/download.html>

### Creating Dockerfile Karaf images

#### Create a Dockerfile

**Update the Dockerfile as bellow**

```
FROM java:8-jdk
MAINTAINER wwwnqloc
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64

ENV KARAF_VERSION=4.2.8

COPY apache-karaf-${KARAF_VERSION}.tar.gz ./

RUN mkdir /opt/karaf; \
    tar --strip-components=1 -C /opt/karaf -xzf apache-karaf-${KARAF_VERSION}.tar.gz; \
    rm apache-karaf-${KARAF_VERSION}.tar.gz;

EXPOSE 1099 8101 44444
ENTRYPOINT ["/opt/karaf/bin/karaf"]
```
* **FROM**: The base image for building a new image. This command must be on top of the dockerfile.
* **MAINTAINER**: Optional, it contains the name of the maintainer of the image.
* **ENV**: Define an environment variable.
* **WORKDIR**: This is directive for CMD command to be executed.
* **COPY**: Copy a file from the host machine to the new docker image. There is an option to use a URL for the file, docker will then download that file to the destination directory.
* **RUN**: Used to execute a command during the build process of the docker image.
* **EXPOSE**: This instruction exposes specified port to the host machine
* **ENTRYPOINT**: Define the default command that will be executed when the container is running.

#### Build docker image

Execute bellow command

```sh
docker build -t karaf_docker .
```

When the command completed successfully, we can check the new image 'karaf_docker' with the docker command below:

```sh
docker images | grep karaf_docker
```

```sh

```

### Deploy your apache karaf container

```sh
docker run ....
```

### Deploy your apache karaf container by docker-compose

Create a docker-compose file ***karaf_docker.yml**

```yml
version: '3.0'
networks:
  karaf_net:
    external: true
services:
    karaf_docker:
        image: karaf_docker
        container_name: karaf_docker
        restart: always
        ports:
            - "1099:1099"
            - "8101:8101"
            - "44444:44444"
        # volumes:
        #    - /home/<user>/docker-mapping/karaf:/opt/karaf/deploy
        stdin_open: true
        tty: true
        networks:
            - karaf_net
```

Start the container by docker-compose

```sh
docker-compose -f karaf_docker.yml up -d
```

And you can check container by command 

```sh
docker ps
```



