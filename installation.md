# Installation

LogBox can be downloaded as a standalone framework or it is included with the latest ColdBox Platform release. The main difference between both versions is the instantiation and usage namespace, the rest is the same.

The best way to install LogBox is using **CommandBox CLI and package manager**.

* [Download LogBox Standalone](https://www.coldbox.org/download)
* [API Docs](https://apidocs.ortussolutions.com/logbox/5.0.0/index.html)

## System Requirements

* ColdFusion 11+
* Lucee 4.5+


## Manual Installation

If you are using LogBox within a ColdBox application context, then LogBox is part of the platform. Just install ColdBox normally. If you are using LogBox standalone, just drop LogBox in your application root or create a mapping called `logbox` that points to the installation folder. If you can run the following snippet, then LogBox is installed correctly:

```java
logbox = new logbox.system.logging.LogBox();
```

## CommandBox Installation

You can leverage [CommandBox](http://www.ortussolutions.com/products/commandbox) to install the standalone version of LogBox

```bash
box install logbox
```

## Namespaces

**Standalone**

`logbox.system.logging`

**ColdBox**

`coldbox.system.logging`

> **Info** In this book we will be using the standalone namespace for all examples.



# Useful Resources

* [LogBox Docs Source](https://github.com/coldbox/logbox-docs)
* [LogBox Planning Board](https://ortussolutions.atlassian.net/browse/LOGBOX)
* [Log4J](http://logging.apache.org/log4j/2.x/)
* [LogStash](http://logstash.net)



