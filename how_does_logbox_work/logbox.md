# LogBox

LogBox is the core framework you need to instantiate in order to work with logging in your application. You have to instantiate it with a `LogBoxConfig` object that will hold your logging configurations. After the library is instantiated and configured you can ask from it a named Logger object so you can start logging or tracing messages.

You have two ways to use LogBox:

* Standalone Framework
* Within a ColdBox application

If you have downloaded LogBox as a standalone framework, then the initial namespace for the core is `logbox.system`. This allows you to use logbox as a standalone framework that is integrated into your proprietary application.

The ColdBox Framework already has an instance of LogBox created for you in every application and it is stored in the main application controller: `controller.getLogBox()`. The namespace within the ColdBox framework is `coldbox.system`.


```javascript
/** Creating LogBox from within a ColdBox Application **/
// Create the config object with an XML configuration file
config = createObject("component","coldbox.system.logging.config.LogBoxConfig").init(expandPath('logbox.xml'));
// Create logbox instance
logBox = createObject("component","coldbox.system.logging.LogBox").init(config);

/** Creating LogBox when used as a stand-alone logging framework **/
// Create the config object with an XML file
config = createObject("component","logbox.system.logging.config.LogBoxConfig").init(expandPath('logbox.xml'));
// Create logbox
logBox = createObject("component","logbox.system.logging.LogBox").init(config);
```
