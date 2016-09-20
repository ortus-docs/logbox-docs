# Using a Logger Object

Once you retrieve a logger object from LogBox, you are ready to start sending messages. We already covered how to dynamically add/remove/list/check appenders from a logger, so let's look at the other methods we have available:

## Utility Methods

* `boolean canLog(numeric level)` : Checks if this logger can log a certain type of severity, there is also a can{severity}() method for each severity level.
* `boolean can{severity}()` : Checks if this logger can log a certain type of severity
* boolean can{severity}()` : Checks if this logger can log a certain type of severity
* `void setCategory(category)` : Set the category name
* `Logger getRootLogger()` : Get the root Logger
* `numeric getLevelMin()` : Get the minimum severity level
* `void setLevelMin(numeric level)` : Set the minimum severity level
* `numeric getLevelMax()` : Get the maximum severity level
* `void setLevelMax(numeric level)` : Set the maximum severity level

## Logging Methods

* `fatal(string message, [any extraInfo=' '])` : Log a fatal message
* `error(string message, [any extraInfo=' '])` : Log an error message
* `warn(string message, [any extraInfo=' '])` : Log a warning message
* `info(string message, [any extraInfo=' '])` : Log an information message
* `debug(string message, [any extraInfo=' '])` : Log a debug message
* `logMessage(string message, numeric severity, [any extraInfo=' '])` : Log any kind of message

As you can probably tell, all logging methods take in a message string an a second argument called `extraInfo`. This `extraInfo` argument can be anything from a string, a structure, a query or whatever. This way you can send in a complex structure that the appenders will serialize into message form or log into its appropriate channel. Thus, `extraInfo` can be very handy when you are building your own custom appenders.

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


## Instance Members

Every logger has access to the following public variables:
* `this.logLevels` : A reference to the `logbox.system.logging.LogLevels class`
