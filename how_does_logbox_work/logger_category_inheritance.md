# Logger Category Inheritance

<h3 style="color:grey">Logger Category Inheritance</h3>


We have a convention for our category names where each category name uses dot-notation according to the components path. Using a class-path convention for our category names allows one to pseudo-inherit for logging levels and appenders! The following example should help clarify this concept.

The overall premise is that when you request a logger with a category name LogBox will search for it's configuration. If LogBox does not find a configuration for the category name it will try to locate its closest ancestor for logging levels and appenders. If LogBox cannot find an ancestor the message will be logged using the root logger information. For example, let's say we define some categories like this:

```javascript
// Configured Appenders: FileAppender, ConsoleAppender
config.category(name="coldbox.system",levelMin=config.logLevels.INFO,appenders="console");
config.error("coldbox.system.plugins");
```

Then, let's say we request the following logger objects:

```javascript
logger = logBox.getLogger("coldbox.system.plugins.BeanFactory");
logger.info("hello info");
logger.error("wow and error occurred");

logger = logBox.getLogger("coldbox.system.interceptors.SES");
logger.info("hello info");
logger.debug("a cool debug message");
```

> <b> Information</b> All example code snippets are using a getLogger('categoryname') call instead of our preferred approach of getLogger(this) because we want to showcase which category we are talking about. Please take this into consideration.


|Category|Configured Levels|Assigned Levels|Appenders|
|--|--|--|--|
|root |FATAL-DEBUG |FATAL-DEBUG |console,file|
|<i>coldbox.system </i>|INFO-DEBUG |INFO-DEBUG |console |
|<i>coldbox.system.plugins </i>|ERROR |ERROR|*|
|<i>coldbox.system.interceptors.SES </i>|coldbox.system.interceptors.SES |INFO-DEBUG from <i>coldbox.system</i> |console from <i>coldbox.system </i>|
|<i>coldbox.system.plugins.BeanFactory </i>|NONE|ERROR from <i>coldbox.system.plugins</i> |*|

Since we requested the category: <i>coldbox.system.plugins.BeanFactory</i>, LogBox tries to locate it, but it has not been defined, so it takes off the last item in the category name. Now it will search for a category of: <i>coldbox.system.plugins</i> via pseudo-inheritance. However, now <i>coldbox.system.plugins</i> has been found and it has been configured to only listen to <i>error</i> messages. Therefore, the <i>coldbox.system.plugins.BeanFactory</i> logger can ONLY log error messages according to it's inherited category. So the <i>info()</i> message will be ignored!

The second logger is called <i>coldbox.system.interceptors.SES</i>, LogBox tries to match a category but fails, so it now searches for a logger called <i>coldbox.system.interceptors</i>. It still cannot find it so it continues up the package chain and finds the <i>coldbox.system</i> logger which has been set with a minimum of <i>DEBUG</i> level and ONLY the console appender. So the only message that gets logged is the <i>logger.debug()</i> message and it will be sent to the console appender.

These examples should give you insight into category inheritance and the power they provide. You can easily turn toggle logging for entire packages with a single category definition. However, this is great only if you follow the dot notation conventions. Below is a sample generic chart sample:


|Category|Configured Levels|Assigned Levels|
|--|--|--|
|root|FATAL-DEBUG |FATAL-DEBUG|
|x |NONE |FATAL-DEBUG from <i>root</i>|
|x.y |INFO |INFO |
|x.y.z |NONE |INFO from <i>x.y</i>|

<h3 style="color:grey"></h3>
