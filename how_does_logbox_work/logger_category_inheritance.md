# Logger Category Inheritance

We have a convention for our category names where each category name uses dot-notation according to the components path. Using a class-path convention for our category names allows one to pseudo-inherit for logging levels and appenders! The following example should help clarify this concept.

The overall premise is that when you request a logger with a category name LogBox will search for it's configuration. If LogBox does not find a configuration for the category name it will try to locate its closest ancestor for logging levels and appenders. If LogBox cannot find an ancestor the message will be logged using the root logger information. For example, let's say we define some appenders like this:

```javascript
// Appenders
config.appender( name="console", class="logbox.system.logging.appenders.ConsoleAppender" );
config.appender( name="file", class="logbox.system.logging.appenders.FileAppender", properties={ filePath="/logs" } )
```

And some categories like this:

```javascript
// Explicit Categories
config.category( name="coldbox.system", levelMin=config.logLevels.INFO, appenders="console" );

// Implicit Categories
config.error( "coldbox.system.plugins" );
// same as
// config.cateogry( name="coldbox.system.plugins", levelMax="ERROR" );
```

Then, let's say we request the following logger objects and logged some info:

```javascript
logger = logBox.getLogger( "coldbox.system.plugins.BeanFactory" );
logger.info( "hello info" );
logger.error( "wow and error occurred" );

logger = logBox.getLogger( "coldbox.system.interceptors.SES" );
logger.info( "hello info" );
logger.debug( "a cool debug message" );
```

> <b> Information</b> All example code snippets are using a `getLogger( "categoryname" )` call instead of our preferred approach of `getLogger( this )` because we want to showcase which category we are talking about. Please take this into consideration.

|Category|Configured Levels|Assigned Levels|Appenders|
|--|--|--|--|
|root |FATAL-DEBUG |FATAL-DEBUG |console,file|
|`coldbox.system `|INFO-DEBUG |INFO-DEBUG |console |
|`coldbox.system.plugins `|ERROR |ERROR|*|
|`coldbox.system.interceptors.SES `|coldbox.system.interceptors.SES |INFO-DEBUG from `coldbox.system` |console from `coldbox.system `|
|`coldbox.system.plugins.BeanFactory `|NONE|ERROR from `coldbox.system.plugins` |*|

Since we requested the category: `coldbox.system.plugins.BeanFactory`, LogBox tries to locate it, but it has not been defined, so it takes off the last item in the category name. Now it will search for a category of: `coldbox.system.plugins` via pseudo-inheritance. However, now `coldbox.system.plugins` has been found and it has been configured to only listen to `error` messages. Therefore, the `coldbox.system.plugins.BeanFactory` logger can ONLY log error messages according to it's inherited category. So the `info()` message will be ignored, and the `error()` message will be sent to both the FileAppender and the ConsoleAppender!

The second logger is called `coldbox.system.interceptors.SES`, LogBox tries to match a category but fails, so it now searches for a logger called `coldbox.system.interceptors`. It still cannot find it so it continues up the package chain and finds the `coldbox.system` logger which has been set with a minimum of `INFO` level and ONLY the console appender. So the messages that get logged is the `logger.info()` and the `logger.debug()` message and they will be sent to the console appender.

These examples should give you insight into category inheritance and the power they provide. You can easily turn toggle logging for entire packages with a single category definition. However, this is great only if you follow the dot notation conventions. Below is a sample generic chart sample:

|Category|Configured Levels|Assigned Levels|
|--|--|--|
|root|FATAL-DEBUG |FATAL-DEBUG|
|x |NONE |FATAL-DEBUG from `root`|
|x.y |INFO |INFO |
|x.y.z |NONE |INFO from `x.y`|




