# Installing LogBox

LogBox can be downloaded as a standalone framework or it is included with the latest ColdBox Platform release. The main difference between both versions is the instantiation and usage namespace, the rest is the same.

* [Download LogBox Standalone](http://www.coldbox.org/download)
* [Download API Docs](http://www.coldbox.org/api)

## Namespaces

**Standalone**

`logbox.system.ioc`

**ColdBox**
`coldbox.system.ioc`

> **Info** In this book we will be using the standalone namespace for all examples.


# Manual Installation

If you are using WireBox within a ColdBox application context, then WireBox is part of the platform. Just install ColdBox normally. If you are using WireBox standalone, just drop WireBox in your application root or create a mapping called `wirebox` that points to the installation folder. If you can run the following snippet, then WireBox is installed correctly:

```
wirebox = new wirebox.system.ioc.Injection();
```

> **Note** Please remember that if you use the standalone version the namespace is `wirebox.system.ioc` and if you use the ColdBox application version it is `coldbox.system.ioc`. From this point on, we will use the standalone namespace for simplicity.
<br>


# CommandBox Installation
You can leverage [CommandBox](http://www.ortussolutions.com/products/commandbox) to install the standalone version of WireBox

```bash
box install wirebox
```
