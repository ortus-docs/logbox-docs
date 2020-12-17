# Installation

LogBox can be downloaded as a standalone framework or it is included with the latest ColdBox Platform release. The main difference between both versions is the instantiation and usage namespace, the rest is the same.

* [Download LogBox Standalone](http://www.coldbox.org/download)
* [Download API Docs](http://www.coldbox.org/api)

## Namespaces

**Standalone**

`logbox.system.logging`

**ColdBox**

`coldbox.system.logging`

> **Info** In this book we will be using the standalone namespace for all examples.

## Manual Installation

If you are using LogBox within a ColdBox application context, then LogBox is part of the platform. Just install ColdBox normally. If you are using LogBox standalone, just drop LogBox in your application root or create a mapping called `logbox` that points to the installation folder. If you can run the following snippet, then LogBox is installed correctly:

```text
logbox = new logbox.system.logging.LogBox();
```

## CommandBox Installation

You can leverage [CommandBox](http://www.ortussolutions.com/products/commandbox) to install the standalone version of LogBox

```bash
box install logbox
```

