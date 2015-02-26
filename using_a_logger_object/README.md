# Using a Logger Object
Once you retrieve a logger object from LogBox, you are ready to start sending messages. We already covered how to dynamically add/remove/list/check appenders from a logger, so let's look at the other methods we have available:

Utility Methods

* <i>boolean canLog(numeric level)</i> : Checks if this logger can log a certain type of severity, there is also a can{severity}() method for each severity level.
* <i>boolean can{severity}()</i> : Checks if this logger can log a certain type of severity
* boolean can{severity}()</i> : Checks if this logger can log a certain type of severity
* <i>void setCategory(category)</i> : Set the category name
* <i>Logger getRootLogger()</i> : Get the root Logger
* <i>numeric getLevelMin()</i> : Get the minimum severity level
* <i>void setLevelMin(numeric level)</i> : Set the minimum severity level
* <i>numeric getLevelMax()</i> : Get the maximum severity level
* <i>void setLevelMax(numeric level)</i> : Set the maximum severity level

Logging Methods

* <i>fatal(string message, [any extraInfo=' '])</i> : Log a fatal message
* <i>error(string message, [any extraInfo=' '])</i> : Log an error message
* <i>warn(string message, [any extraInfo=' '])</i> : Log a warning message
* <i>info(string message, [any extraInfo=' '])</i> : Log an information message
* <i>debug(string message, [any extraInfo=' '])</i> : Log a debug message
* <i>logMessage(string message, numeric severity, [any extraInfo=' '])</i> : Log any kind of message

As you can probably tell, all logging methods take in a message string an a second argument called <i>extraInfo</i>. This <i>extraInfo</i> argument can be anything from a string, a structure, a query or whatever. This way you can send in a complex structure that the appenders will serialize into message form or log into its appropriate channel. Thus, <i>extraInfo</i> can be very handy when you are building your own custom appenders.

```javascript
// setting some messages
myLogger = logBox.getLogger(this); //"com.model.dao"

myLogger.info("I just created my first logger");

try{
	data = dao.getDBData();
}
catch(Any e){
	myLogger.error("Something really died on my dbdata method: #e.message# #e.detail#",e.tagContext);
}
```

I hope that by now you understand the basics of loggers and how easy it is to use them.


<h3 style="color:grey">Instance Members</h3>

Every logger has access to the following public variables:
* <i>this.logLevel</io> : A reference to the <i>coldbox.system.logging.LogLevels class</i>
