---
layout: post
title: Dockerizing an Apache Karaf image
category: Karaf, OSGI, Apache Karaf, Docker
tags: [Karaf, OSGI, Apache Karaf, Docker]
active: true
---


### 1. Download karaf from <http://karaf.apache.org/download.html>

### 2. Creating Dockerfile Karaf images

#### Create a Dockerfile

Update the Dockerfile as bellow

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

```sh
nqloc@localhost:~/xxx/karaf_docker$ docker build -t karaf_docker .
Sending build context to Docker daemon  22.44MB
Step 1/8 : FROM java:8-jdk
 ---> d23bdf5b1b1b
Step 2/8 : MAINTAINER wwwnqloc
 ---> Running in a57c104eae0a
 ---> 431f025ac316
Removing intermediate container a57c104eae0a
Step 3/8 : ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
 ---> Running in 117d8ff97660
 ---> 3b51995aa09e
Removing intermediate container 117d8ff97660
Step 4/8 : ENV KARAF_VERSION 4.2.8
 ---> Running in b6f34427a85e
 ---> 8acbd587d47e
Removing intermediate container b6f34427a85e
Step 5/8 : COPY apache-karaf-${KARAF_VERSION}.tar.gz ./
 ---> 48a2997ea6c0
Step 6/8 : RUN mkdir /opt/karaf;     tar --strip-components=1 -C /opt/karaf -xzf apache-karaf-${KARAF_VERSION}.tar.gz;     rm apache-karaf-${KARAF_VERSION}.tar.gz;
 ---> Running in c21af6cb95ed
 ---> 57238ddee096
Removing intermediate container c21af6cb95ed
Step 7/8 : EXPOSE 1099 8101 44444
 ---> Running in ceb798157713
 ---> 7e61876b0b88
Removing intermediate container ceb798157713
Step 8/8 : ENTRYPOINT /opt/karaf/bin/karaf
 ---> Running in b335b3b247d8
 ---> fd6f500a7b09
Removing intermediate container b335b3b247d8
Successfully built fd6f500a7b09
Successfully tagged karaf_docker:latest
```

When the command completed successfully, we can check the new image 'karaf_docker' by command **docker images | grep karaf_docker**

```sh
nqloc@localhost:~/xxx/karaf_docker$ docker images | grep karaf_docker
karaf_docker                           latest                fd6f500a7b09        2 minutes ago       692MB
```

### 3. Deploy your apache karaf container

Deploy the **karaf_docker** container by command **docker run karaf_docker -d**

```sh
docker run karaf_docker -d
        __ __                  ____      
       / //_/____ __________ _/ __/      
      / ,<  / __ `/ ___/ __ `/ /_        
     / /| |/ /_/ / /  / /_/ / __/        
    /_/ |_|\__,_/_/   \__,_/_/         

  Apache Karaf (4.2.8)

Hit '<tab>' for a list of available commands
and '[cmd] --help' for help on a specific command.
Hit '<ctrl-d>' or type 'system:shutdown' or 'logout' to shutdown Karaf.

karaf@root()> 
```

### Deploy your apache karaf container by docker-compose

Create a docker-compose file **karaf_docker.yml**

```yml
version: '3.0'
services:
    karaf_docker:
        image: karaf_docker
        container_name: karaf_docker
        restart: always
        ports:
            - "1099:1099"
            - "8101:8101"
            - "44444:44444"
        stdin_open: true
        tty: true
```

Start the container by docker-compose. Execute command **docker-compose -f karaf_docker.yml up -d**

Then you can check docker container by command **`docker ps | grep karaf_docker`**

```sh
docker ps | grep karaf_docker
d35fe07b0493        karaf_docker        "/opt/karaf/bin/karaf"   2 minutes ago       Up 2 minutes        0.0.0.0:1099->1099/tcp, 0.0.0.0:8101->8101/tcp, 0.0.0.0:44444->44444/tcp   karaf_docker
```

### 4. Apache Karaf hot deploy

(TBU)

