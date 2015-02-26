# XML Configuration
You can also configure LogBox with an XML file. All you need to do is create a LogBox xml file and instantiate the config object with the location of such config file:

```javascript
config = createObject("component","coldbox.system.logging.config.LogBoxConfig").init(expandPath("/config/logbox.xml"));
```

However, if you have your XML in a variable already, maybe you read it from a database or other location, you can still use it by calling the config object's parseAndLoad() method.

```javascript
//Get the xml document from somewhere.
xmlDoc = dbService().getLogBoxConfig();
//create the log box config object
config = createObject("component","coldbox.system.logging.config.LogBoxConfig").init();
config.parseAndLoad(xmlDoc);
```

Sample <i>logbox.xml</i> file:

```javascript
<?xml version="1.0" encoding="UTF-8"?>
<LogBox xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="http://www.coldbox.org/schema/LogBoxConfig_1.4.xsd">

	<-- <Appender Definitions -->
	<Appender name="myconsole" class="coldbox.system.logging.appenders.ConsoleAppender" />
	<Appender name="MyCF" class="coldbox.system.logging.appenders.CFAppender" layout="model.myLayout">
		<Property name="fileName">MyAppLogName</Property>
	</Appender>
	<Appender name="FileAppender" class="coldbox.system.logging.appenders.AsyncRollingFileAppender" levelMax="DEBUG">
		<Property name="filePath">/coldbox/testing/logging/tmp</property>
		<Property name="fileMaxSize">3</Property>
		<Property name="fileMaxArchives">2</Property>
	</Appender>

	<-- <Root Logger -->
		<-- <Root All Appenders
		<Root levelMin="0" levelMax="4" appenders="*">
	-->
	<Root levelMin="0" levelMax="4">
		<Appender-ref ref="myconsole" />
		<Appender-ref ref="MyCF" />
		<Appender-ref ref="FileAppender" />
	</Root >

	<-- <Very advanced category -->
	<Category name="MySES" levelMin="3" levelMax="4">
		<Appender-ref ref="myconsole" />
	</Category>

	<Category name="com.model.services" levelMax="3" appenders="MyCF" />
	<Category name="com.model.dao" levelMax="2" appenders="*" />
</LogBox>
```
As you can see, you need to create a root element called LogBox with the following child elements:

* <i>&lt;Appender&gt;</i> : an appender definition. Can be 1 or more elements.
    * <i>@name</i> : The name of the appender (required)
    * <i>@class</i> : The class of the appender (required)
    * <i>@layout</i> : The layout class to use for rendering the messages (optional)
    * <i>@levelMin</i> : The default minimum log level. (optional)
    * <i>@levelMax</i> : The default maximum log level. (optional)
* <i>&lt;Root&gt;</i> : The root logger element. Can only be 1 defined.
    * <i>@levelMin</i> : The default minimum log level. (optional)
    * <i>@levelMax</i> : The default maximum log level. (optional)
    * <i>@appenders</i> : An optional list of appenders for the root logger or* for all appenders. (optional)
    * <i>&lt;Appender-ref&gt;</i> : If you do not like to use a list for the appenders, you can use this element to add appenders to the root logger. You can have 0 or more of these elements defined.
        * <i>@ref</i> : The name of the appender to reference.
* <i>&lt;Category&gt;</i> : A category definition element. You can have 0 or more of these defined.
    * <i>@name</i> : The name of the category
    * <i>@levelMin</i> : The default minimum log level. (optional)
    * <i>@appenders</i> : An optional list of appenders for this category or* for all appenders. (optional)
        * <i>@ref</i> : The name of the appender to reference.

> <b>Information</b>

Note: All the levelMin and levelMax attributes can either be the numeric representation of the severity or the fully qualified name you can see in the severity table.

