---
layout: post
title: Apache Karaf
category: [Karaf, OSGI, Apache Karaf]
tags: [Karaf, OSGI, Apache Karaf]
active: true
language: en
---

> Apache Karaf is a small OSGi based runtime which provides a lightweight container onto which various components and applications can be deployed

### Defination

#### What is it in details?

* Karaf is a **platform** that allow you to deploy your application
* You can **install/uninstall/start/stop** your application in several easy way
* You can **replace/update** it and you can change it on the fly

#### What is an application?

* An application is a composition of modules
* Each module can depend from other modules of application or form other modules of the container

#### What is a module?

* A module is a bundle
* Bundle is a jar with a Manifest than that one

#### How a bundle interact?

* Each bundle can register one or more service
* Each service can be retrieved by other bundle
* Each service can obtain the reference of other services

#### What is a service?

* A service is a self-contained unit of functionality

OSGI service example

```java
// file CustomerService.java
package com.www.customer.service;

public interface CustomerService {
	Customer lookupCustomer(String customerId);
}

// file CustomerServiceImpl.java
package com.www.customer.service.impl;

public class CustomerServiceImpl implements CustomerService {
	
	public CustomerServiceImpl() {
		// constructor
	}
	
	public void init() {
		// define some init steps here
	}
	
	public void destroy() {
		// define some destroy steps here
	}
	
	public Customer lookupCustomer(String customerId) {
		Customer customer = new Customer();
		customer.setFirstName("Loc");
		customer.setLastName("Nguyen");
		customer.setPhoneNumber("+84978909371");
		customer.setId(customerId);
		return customer;
	}
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<blueprint
    xmlns="http://www.osgi.org/xmlns/blueprint/v1.0.0">
    <bean id="customerServiceImpl" class="com.www.customer.service.impl.CustomerServiceImpl" init-method="init" destroy-method="destroy"></bean>
    <service ref="customerServiceImpl" interface="com.www.customer.service.CustomerService"></service>
</blueprint>
```

#### What is a karaf feature?

* A group of relatived bundles

### How to start a Karaf server

* Download karaf from <http://karaf.apache.org/download.html>
* Extract the downloaded file
* Add or update **KARAF_HOME env**
* Run command **bin\karaf.bat** (for windows) or **bin/karaf** (for Linux)

```sh
        __ __                  ____
       / //_/____ __________ _/ __/
      / ,<  / __ `/ ___/ __ `/ /_
     / /| |/ /_/ / /  / /_/ / __/
    /_/ |_|\__,_/_/   \__,_/_/

  Apache Karaf (4.2.0)

Hit '<tab>' for a list of available commands
and '[cmd] --help' for help on a specific command.
Hit '<ctrl-d>' or type 'system:shutdown' or 'logout' to shutdown Karaf.

karaf@root()>
```

#### Directory structure

* /bin: control scripts to start, stop, login, …

* /examples: contains several examples to start with Apache Karaf

* /etc: configuration files

* /data: working directory

  * /data/cache: OSGi framework bundle cache

  * /data/generated-bundles: temporary folder used by the deployers

  * /data/log: log files

* /deploy: hot deploy directory

* /instances: directory containing `[instances|instances]`

* /lib: contains libraries

  * /lib/boot: contains the system libraries used at Karaf bootstrap

  * /lib/endorsed: directory for endorsed libraries

  * /lib/ext: directory for JRE extensions

* /system: OSGi bundles repository, laid out as a Maven 2 repository

#### Stop karaf server (3 ways)

* Enter **^D** in the console
* Enter **system:shutdown** in the console
* Enter **halt** in the console (this is **system:shutdown**'s alias)

#### Cleaning the Karaf state

* Just delete the **data directory** when Karaf is not running
* Start karaf with argument **clean** (e.g bin/karaf clean)

### How to deploy an application in Karaf

### Karaf commands

<https://cwiki.apache.org/confluence/display/KARAF/4.1.+Console+and+Commands>

### Karaf and Web

### Karaf examples

* [Karaf bundle example](https://nqloc.github.io)
* [Karaf cfx example](https://nqloc.github.io)
* [Dockerizing an Apache Karaf image] (https://nqloc.github.io)

### Reference

* <https://www.slideshare.net/CristianoCostantini/modular-java-with-osgi-and-karaf>
