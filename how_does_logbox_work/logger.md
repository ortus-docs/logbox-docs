# Logger

The logger component is a named entity that you use to log or trace messages with. The logger is responsible for deciding if the severity level of the message is adequate for redirecting to a destination via any of its attached appenders. If the logger component deems the message qualifies to be redirected the logger will route the message(s) to the applicable appender(s) for delivery. There are two types of loggers in LogBox:

```javascript
// Configuring some appenders and the root logger
config.appender( 
    name="Console", 
    class="logbox.system.logging.appenders.ConsoleAppender"
);
// root logger
config.root(
    levelMin=config.logLevels.FATAL, 
    levelMax=config.logLevels.INFO, 
    appenders="Console"
);

// Or using simple CFC
logBox = {
	appenders = {
		Console = { class="logbox.system.logging.appenders.ConsoleAppender" }
	},
	root = {levelMin="FATAL", levelMax="INFO", appenders="*"}
}

//Asking logbox for the root logger
Logger = logBox.getRootLogger();
```

Loggers are named entities. The name you provide for a logger is refereed to as the logger's category name. This category can be the name of the component or class you are logging messages from or it can be any unique name you desire to distinguish the message being logged.

> <b>Important</b> It is best practice to name your categories with the exact path notation of the component. Ex: `logbox.system.plugins.BeanFactory`. For simplicity, you can just pass in the object reference and LogBox will figure out the name for you. Example: `logger = logBox.getLogger(this);`

Let's say that I want to log messages in the SES interceptor whose class is `coldbox.system.interceptors.SES`. Then I would do the following to request a logger for usage in my SES interceptor:

```javascript
// A possible approach to defining a category name.
// Declaring a logger while explicitly defining the category name.
logger = logBox.getLogger('coldbox.system.interceptors.SES');
//log an info message
logger.info("Customer deposited fifty billion dollars into your account.");
```

However, you can simplify the code above by passing the instance of where you are logging from. LogBox will then use the object's fully qualified name, via inspection, to define the logger's category name. This approach is simpler and is our preferred approach. Passing this will support refactorings and object name changes without burdening your application.

> **Important** To stay true to our best practice recommendation of passing this to the `getLogger()` method your CFC must have a name attribute within the component declaration. Example:

```javascript
// The prefered approach to defining a category name.
// Declaring a logger while allowing LogBox to implicitly define the category name via introspection.
logger = logBox.getLogger(this);

//log an info message
logger.info("Customer deposited fifty billion dollars into your account. Again.");
```

The above two lines of code illustrate the simplicity of getting a named logger from LogBox. Two important question are: What severity messages will the logger log? and What is the destination (or destinations) of these messages? In the above example we did not explicitly configure an answer to these two questions while we created a logger for `coldbox.system.interceptors.SES`, so, LogBox will use the root logger. Thus it will use the root logger's severity level range and configured appenders. 

```javascript
//register a list of categories that respond to FATAL messages
//only using the root logger's appenders
config.fatal("coldbox.system.controller","mycfc","com.model.mycfc");

// log for errors only using the root logger's appenders
config.error("mycfc","com.model.mycfc");

//log for info only using the root logger's appenders
config.info("org.model.component");

//log all email service messages to the MyLogFileAppender and the Console.
config.category(name="org.model.EmailService",appenders="MyLogFileAppender,Console");
```

This is the same but using the simplified Data CFC Approach:

```javascript
logBox = {
	//register a list of categories that respond to FATAL messages
	fatal = ["coldbox.system.controller","mycfc","com.model.mycfc"],
	// log for errors only using the root logger's appenders
	error = ["mycfc","com.model.mycfc"],
	//log for info only using the root logger's appenders
	info = ["org.model.component"],

	//Register categories granularly:
	categories = {
		"com.model.myservice" = {levelMax="ERROR",appenders="MyTwit" },
		"org.model.EmailService" = {appenders="MyLogFileAppender,Console"}
	}
};
```
You have the option to create granular categories where you can choose a level range and/or appenders, or easily tag a category to listen to only one specific type of message using the severity methods in the config object. The methods available are the same as the Severity column in the severity levels chart.

