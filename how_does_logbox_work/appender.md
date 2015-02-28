# Appender

An appender is an object that LogBox uses to log statements to a destination repository. All appenders act as destinations that can include: databases, JMS, files, consoles, sockets, etc. The appender has the responsibility of taking the logged message and persisting the message or sending the message to an external service. LogBox comes bundled with the following appenders that can be found in the package coldbox.system.logging.appenders:

|Appender|Description|
|--|--|
|AsyncFileAppender |An Asynchronous file appender.|
|AsyncDBAppender |An Asynchronous database appender.|
|AsyncRollingFileAppender |An Asynchronous file appender that can do file rotation and archiving.|
|CFAppender |Will deliver messages to the coldfusion logs.|
|ColdBoxTracerAppender |Will deliver messages to the ColdBox Tracer Panel in the ColdBox debugger.|
|ConsoleAppender |Will deliver messages to the server's console via system.out |
|DBAppender|Will deliver messages to a database table. It can auto create the table for you. |
|EmailAppender |Will deliver messages to any email address.|
|FileAppender |Will deliver messages a file. |
|RollingFileAppender |A file appender that can do file rotation and archiving.|
|ScopeAppender |Will deliver messages to any ColdFusion variable scope.|
|SocketAppender|Will connect to any server socket and deliver messages. |
|TracerAppender |Will deliver messages to the ColdFusion tag cftrace. |

You can configure LogBox to use one or all of these appenders at any point in time. You can even register as many instances of any appender by defining a unique name for each. Here are examples of how one can configure appenders programmatically or via the simple configuration CFC:


**Programmatic Approach**

```javascript
//Adding appenders
props = {
	filePath = expandPath("/logbox/testing/cases/logging/tmp"),
	autoExpand=false,
	fileMaxArchives=1,
	fileMaxSize=3000
};

config.appender(
	name='MyAsyncFile',
	class="logbox.system.logging.appenders.AsyncRollingFileAppender",
	properties=props
);

//socket
props = { host="localhost", timeout="3", port="444", persistConnection=false };
config.appender(
	name='SocketAppender',
	class="logbox.system.logging.appenders.SocketAppender",
	properties=props
);
```

**Configuration CFC approach**

```javascript
function configure(){

	logBox = {
		// Register Appenders
		appenders = {
			MyAsycFile = {
				class="logbox.system.logging.appenders.AsyncRollingFileAppender",
				properties={
					filePath=expandPath("/logbox/testing/cases/logging/tmp"),
					autoExpand=false,
					fileMaxArchives=1,
					fileMaxSize=3000
				}
			},

			SocketAppender = {
				class="logbox.system.logging.appenders.SocketAppender",
				properties = {
					host="localhost",
					timeout="3",
					port="444",
					persistConnection=false
				}
			}

		}
	};
}
```

Another feature of a LogBox appender is that you can <i>extend</i> them or create new ones simply by leveraging the LogBox API. To customize LogBox appenders for your own unique needs you would simply extend the core appender class: <i>coldbox.system.logging.AbstractAppender</i> and implementing the <i>init()</i> and <i>logMessage()</i> methods. Extending LogBox will be reviewed in greater detail over the next few sections.
