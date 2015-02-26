# Adding Appenders

The first thing you need to do in your config object is add appenders. Each appender is added via the appender() method.

<i>public void appender(string name, string class, [struct properties], string layout=)</i>

Parameters:
* name - A unique name for the appender to register. Only unique names can be registered per instance.
* class - The appender's class to register. We will create, init it and register it for you.
* properties - The structure of properties to configure this appender with.
* layout - The layout class path to use in this appender for custom message rendering.
* levelMin : The numerical or English word of the minimal logging level (optional, defaults to 0)
* levelMax : The numerical or English word of the maximum logging level (optional, defaults to 4)

```javascript
config.appender(name="CFConsole",class="coldbox.system.logging.appenders.ConsoleAppender");
config.appender(name="MyCF",class="coldbox.system.logging.appenders.CFAppender");

props = {host="localhost",timeout="3",port="444",persistConnection=false};
config.appender(name="SocketBaby",class="coldbox.system.logging.appenders.SocketAppender",properties=props);

props = {filePath='/logs',fileName='Test'};
config.appender(name='Fileapp',
			    class="coldbox.system.logging.appenders.FileAppender",
				properties=props,
			    layout="model.logging.MyFileLayout");
```


