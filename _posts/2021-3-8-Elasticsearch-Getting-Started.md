---
layout: post
title: Elasticsearch: Getting Started
category: Elasticsearch
tags: [Elasticsearch]
active: true
language: en
---

> **WebDav** Initially released in 2010, Elasticsearch (sometimes dubbed ES) is a modern search and analytics engine which is based on Apache Lucene content authoring operations.

## What is Elasticsearch?
* A modern search and analytics engine which is based on Apache Lucene
* Completely open source and built with Java
* NoSQL database

## Install Elasticsearch
### Install Elasticsearch from archive on Linux or MacOS
https://www.elastic.co/guide/en/elasticsearch/reference/7.11/targz.html
### Install Elasticsearch with .zip on Windows
https://www.elastic.co/guide/en/elasticsearch/reference/7.11/zip-windows.html
### Install Elasticsearch with Debian Package
https://www.elastic.co/guide/en/elasticsearch/reference/7.11/deb.html
### Install Elasticsearch with RPM
https://www.elastic.co/guide/en/elasticsearch/reference/7.11/rpm.html
### Install Elasticsearch with Windows MSI Installer
https://www.elastic.co/guide/en/elasticsearch/reference/7.11/windows.html
### Install Elasticsearch on macOS with Homebrew
https://www.elastic.co/guide/en/elasticsearch/reference/7.11/brew.html
### Install Elasticsearch with Docker
#### Pull the image
docker pull elasticsearch
#### Starting a single node cluster with Docker
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch
#### Starting a multi-node cluster with Docker Compose
Create a docker-compose.yml file
```yml
version: '2.2'
services:
  es01:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.11.1
    container_name: es01
    environment:
      - node.name=es01
      - cluster.name=es-docker-cluster
      - discovery.seed_hosts=es02,es03
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data01:/usr/share/elasticsearch/data
    ports:
      - 9200:9200
    networks:
      - elastic
  es02:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.11.1
    container_name: es02
    environment:
      - node.name=es02
      - cluster.name=es-docker-cluster
      - discovery.seed_hosts=es01,es03
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data02:/usr/share/elasticsearch/data
    networks:
      - elastic
  es03:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.11.1
    container_name: es03
    environment:
      - node.name=es03
      - cluster.name=es-docker-cluster
      - discovery.seed_hosts=es01,es02
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data03:/usr/share/elasticsearch/data
    networks:
      - elastic

volumes:
  data01:
    driver: local
  data02:
    driver: local
  data03:
    driver: local

networks:
  elastic:
    driver: bridge
```

Set vm.max_map_count to at least 262144
sudo sysctl -w vm.max_map_count=262144

## Configuring Elasticsearch
sudo vim /etc/elasticsearch/elasticsearch.yml
network.host: "localhost"
http.port:9200

## Creating an Elasticsearch Index
Indexing is the process of adding data to Elasticsearch.

## Elasticsearch Querying

## Removing Elasticsearch Data


## Summary

* Provide a simple solution for file storage
* Support many clients
* Strong support authentication, file locking, versioning
* Free
* Easy to use

## Reference
https://logz.io/blog/elasticsearch-tutorial/
