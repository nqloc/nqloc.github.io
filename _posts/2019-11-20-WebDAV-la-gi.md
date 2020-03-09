---
layout: post
title: WebDAV là gì
category: WebDAV
tags: [WebDAV]
active: true
language: en
---

> **WebDav** (**Web**-base **D**istributed **A**uthoring and **V**ersioning) is an extension of the Hypertext Transfer Protocol (HTTP) that allows clients to perform remote Web content authoring operations.

## Why choose WebDAV?

* Operating system integration
* Open source
* Close integration with web services
* Version Control
* Transport encryption
* Remote access
* Centralized storage
* File locking

## WebDAV as a microservice

![](/images/posts/webdav/webdav_in_microservice.png)

## WebDAV Protocol Methods

* **COPY** copy a resource
* **MOVE** move a resource
* **MKCOL** create a collection, for example, a folder
* **PROPFIND** retrieve properties stored as XML
* **PROPPATCH** change and/or remove properties
* **LOCK** put a lock on a resource
* **UNLOCK** remove a lock from a resource

## WebDAV server

![](/images/posts/webdav/webdav_server_support.png)


## WebDAV client

![](/images/posts/webdav/webdav_client_support.png)

**Access by web browser**

![](/images/posts/webdav/webdav_client_browser.png)

**Map Network Drive in Windows**

![](/images/posts/webdav/webdav_client_map_network_drive.png)


## Build WebDAV server with Apache

* Enable DAV mod (in httpd.conf)

* Create User & Password (in webdav.conf)

* Configure WebDAV folder (in webdav.conf)


![](/images/posts/webdav/webdav_server_config.png)


## Summary

* Provide a simple solution for file storage
* Support many clients
* Strong support authentication, file locking, versioning
* Free
* Easy to use

## Reference
