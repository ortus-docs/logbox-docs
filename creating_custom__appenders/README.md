# Creating Custom  Appenders
In order to create your own appenders, you will have to create a cfc that extends `logbox.system.logging.AbstractAppender` and implement the following methods:

|Method|Description|
|---|---|
|`init()`|Your constructor. Make sure to call `super.init( argumentCollection=arguments );`|
|`logMessage()`|The method that is called when a message is received.|
|`onRegistration()`|An interceptor that fires when the appender gets created and initialized. It can be used for preparing the appender for operation.|
|`onUnRegistration()`|An interceptor that fires when the appender is removed from a logger.|

## `init()`

The signature of the init method is the following:

```javascript
<---  Init --->
<cffunction name="init" access="public" returntype="AbstractAppender" hint="Constructor called by a Concrete Appender" output="false" >
	<---  ************************************************************* --->
	<cfargument name="name" 		type="string"  required="true" hint="The unique name for this appender."/>
	<cfargument name="properties" 	type="struct"  required="false" default="#structnew()#" hint="A map of configuration properties for the appender"/>
	<cfargument name="layout" 		type="string"  required="false" default="" hint="The layout class to use in this appender for custom message rendering."/>
	<cfargument name="levelMin"  	type="numeric" required="false" default="0" hint="The default log level for this appender, by default it is 0. Optional. ex: LogBox.logLevels.WARN"/>
	<cfargument name="levelMax"  	type="numeric" required="false" default="4" hint="The default log level for this appender, by default it is 5. Optional. ex: LogBox.logLevels.WARN"/>
	<---  ************************************************************* --->

</cffunction>
```

As you can see each appender receives a `name`, a structure of `properties`, an optional `layout` class, and an optional `levelMin` and `levelMax` severity levels. The `properties` and `layout` are both optional, but you must call the `super.init( argumentCollection = arguments )` method in order to have full ok operation on the appender. You can then do your own constructor as you see fit. Here is an example:

```javascript
<---  Constructor --->
<cffunction name="init" access="public" returntype="FileAppender" hint="Constructor" output="false">
	<---************************************************************** --->
	<cfargument name="name" 		type="string"  required="true" hint="The unique name for this appender."/>
	<cfargument name="properties" 	type="struct"  required="false" default="#structnew()#" hint="A map of configuration properties for the appender"/>
	<cfargument name="layout" 	type="string"  required="true"  default="" hint="The layout class to use in this appender for custom message rendering."/>
	<cfargument name="levelMin"  	type="numeric" required="false" default="0" hint="The default log level for this appender, by default it is 0. Optional. ex: LogBox.logLevels.WARN"/>
	<cfargument name="levelMax"  	type="numeric" required="false" default="4" hint="The default log level for this appender, by default it is 5. Optional. ex: LogBox.logLevels.WARN"/>
        <---************************************************************** --->
	<cfscript>
		super.init(argumentCollection=arguments);

		// Setup Properties
		if( NOT propertyExists("filepath") ){
			$throw(message="Filepath property not defined",type="FileAppender.PropertyNotFound");
		}
		if( NOT propertyExists("autoExpand") ){
			setProperty("autoExpand",true);
		}
		if( NOT propertyExists("filename") ){
			setProperty("filename",getName());
		}
		if( NOT propertyExists("fileEncoding") ){
			setProperty("fileEncoding","UTF-8");
		}

		// Setup the log file full path
		instance.logFullpath = getProperty("filePath");
		// Clean ending slash
		if( right(instance.logFullpath,1) eq "/" OR right(instance.logFullPath,1) eq "\"){
			instance.logFullPath = left(instance.logFullpath, len(instance.logFullPath)-1);
		}
		instance.logFullPath = instance.logFullpath & "/" & getProperty("filename") & ".log";

		// Do we expand the path?
		if( getProperty("autoExpand") ){
			instance.logFullPath = expandPath(instance.logFullpath);
		}

		//lock information
		instance.lockName = getname() & "logOperation";
		instance.lockTimeout = 25;

		return this;
	</cfscript>
</cffunction>
```

## `logMessage()`

The signature of the `logMessage` method is the following:

```javascript
<---  logMessage --->
<cffunction name="logMessage" access="public" output="false" returntype="void">
	<cfargument name="logEvent" type="logbox.system.logging.LogEvent" required="true" hint="The logging event to log.">
</cffunction>
```

As you can see it is a very simple method that receives a LogBox logging event object. This object keeps track of the following properties with its appropriate getters and setters:

* `timestamp`
* `category`
* `message`
* `severity`
* `extraInfo`

You can then use this logging event object to log to whatever destination you want. Here is a snippet from our scope appender:

```javascript
<---  Log Message --->
<cffunction name="logMessage" access="public" output="true" returntype="void" hint="Write an entry into the appender.">
	<---************************************************************** --->
	<cfargument name="logEvent" type="logbox.system.logging.LogEvent" required="true" hint="The logging event"/>
	<---************************************************************** --->
	<cfscript>
		var logStack = "";
		var entry = structnew();
		var limit = getProperty('limit');
		var loge = arguments.logEvent;

		// Verify storage
		ensureStorage();

		// Check Limits
		logStack = getStorage();

		if( limit GT 0 and arrayLen(logStack) GTE limit ){
			// pop one out, the oldest
			arrayDeleteAt(logStack,1);
		}

		// Log Away
		entry.id = createUUID();
		entry.logDate = loge.getTimeStamp();
		entry.appenderName = getName();
		entry.severity = severityToString(loge.getseverity());
		entry.message = loge.getMessage();
		entry.extraInfo = loge.getextraInfo();
		entry.category = loge.getCategory();

		// Save Storage
		arrayAppend(logStack, entry);
		saveStorage(logStack);
	</cfscript>
</cffunction>
```

## `onRegistration()` & `onUnregistration()`

Finally, both the `onRegistration` and `onUnregistration` methods have to be void methods with no arguments.

```javascript
<cffunction name="onRegistration" access="public" hint="Runs after the appender has been created and registered. Implemented by Concrete appender" output="false" returntype="void">
</cffunction>

<cffunction name="onUnRegistration" access="public" hint="Runs before the appender is unregistered from LogBox. Implemented by Concrete appender" output="false" returntype="void">
</cffunction>
```

These are great for starting or stopping your appenders if they so need to. Here is a sample from our socket appender:

```javascript
<---  onRegistration --->
<cffunction name="onRegistration" output="false" access="public" returntype="void" hint="When registration occurs">
	<cfif getProperty("persistConnection")>
		<cfset openConnection()>
	</cfif>
</cffunction>

<---  onRegistration --->
<cffunction name="onUnRegistration" output="false" access="public" returntype="void" hint="When Unregistration occurs">
	<cfif getProperty("persistConnection")>
		<cfset closeConnection()>
	</cfif>
</cffunction>
```
