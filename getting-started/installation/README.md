# Installation

LogBox can be downloaded as a standalone framework or included with the latest ColdBox Platform release. The main difference between both versions is the instantiation and usage namespace; the rest is the same.

The best way to install LogBox is by using **CommandBox CLI and package manager**.

* [Download LogBox Standalone](https://www.forgebox.io/view/logbox#versions)
* [API Docs](https://apidocs.ortussolutions.com/logbox/current)

## System Requirements

* ColdFusion 2018+
* Lucee 5+

## ColdBox Installation

If you are using LogBox within a ColdBox application context, then LogBox is part of the platform.  Just configure it via the `config/LogBox.cfc` and you are ready to roll.

## Standalone Installation

You can leverage [CommandBox](http://www.ortussolutions.com/products/commandbox) to install the standalone version of LogBox

```bash
# Latest CommandBox
box install logbox

# Bleeding Edge
box install logbox@be
```

#### Mappings

You will need the following mappings that all point to the folder you installed `logbox` into:

```cfscript
this.mappings[ "/logbox" ] = "path.to.logbox";
```

This will ensure that the appropriate libraries can find each other.

{% hint style="danger" %}
Remember that this only applies to the standalone approach.
{% endhint %}

&#x20;If you can run the following snippet, then LogBox is installed correctly:

```java
logbox = new logbox.system.logging.LogBox();
```

## Namespaces

**Standalone**

`logbox.system.logging`

**ColdBox**

`coldbox.system.logging`

