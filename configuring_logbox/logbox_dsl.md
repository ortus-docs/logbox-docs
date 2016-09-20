# LogBox DSL

In order to create a simple data CFC, just create a CFC with one required method on it called configure where you will define the logging configuration data:

```javascript
**
* A LogBox configuration data object
*/
component{

	function configure(){
		logBox={

		};
	}
}
```

## Base Config

Once you have this shell, you will create a `logBox` variable in the `variables` scope that must be a structure with the following keys:

|Key|Description|
|--|--|
|appenders |A structure where you will define appenders|
|root |A structure where you will configure the root logger|
|categories |A structure where you can define granular categories (OPTIONAL)|
|DEBUG|An array that will hold all the category names to place under the DEBUG logging level (OPTIONAL)|
|INFO |An array that will hold all the category names to place under the INFO logging level (OPTIONAL)|
|WARN |An array that will hold all the category names to place under the WARN logging level (OPTIONAL)|
|ERROR|An array that will hold all the category names to place under the ERROR logging level (OPTIONAL)|
|FATAL |An array that will hold all the category names to place under the FATAL logging level (OPTIONAL)|
|OFF|An array that will hold all the category names to not log at all (OPTIONAL)|

### Appenders

To define an appender you must define a struct with a key value which is the internal name of the appender.  Each appender name must be unique.  You configure each appender with the following keys:

|Key|Description|
|--|--|
|class|The class path of the appender|
|properties|The properties struct for the appender (OPTIONAL)|
|layout|The layout class path of the layout object to use (OPTIONAL)|
|levelMin|The numerical or English word of the minimal logging level (OPTIONAL, defaults to 0 [FATAL])|
|levelMax|The numerical or English word of the maximum logging level (OPTIONAL, defaults to 4 [DEBUG])|

### Root Logger

To configure the root logger use the following keys:

|Key|Description|
|--|--|
|levelMin|The numerical or English word of the minimal logging level (OPTIONAL, defaults to 0 [FATAL])|
|levelMax|The numerical or English word of the maximum logging level (OPTIONAL, defaults to 4 [DEBUG])|
|appenders|A string list of the appenders to use for logging|

### Categories

To define categories you must define a struct with a key value which is the internal name of the category. Each category name must be unique. You configure each category with the following keys:

|Key|Description|
|--|--|
|levelMin|The numerical or English word of the minimal logging level (OPTIONAL, defaults to 0 [FATAL])|
|levelMax|The numerical or English word of the maximum logging level (OPTIONAL, defaults to 4 [DEBUG])|
|appenders|A string list of the appenders to use for logging (OPTIONAL, defaults to *)|

As you might notice the name of the keys on all the structures match 100% to the programmatic methods you can also use to configure logBox. So when in doubt, refer back to the argument names.

#### Example Configuration

```javascript
logBox = {
	// Appenders
	appenders = {
		appenderName = {
			class="class.to.appender",
			layout="class.to.layout",
			levelMin=0,
			levelMax=4,
			properties={
				name  = value,
				prop2 = value 2
			}
	},
	// Root Logger
	root = { levelMin="FATAL", levelMax="DEBUG", appenders="*" },
	// Granualr Categories
	categories={
		"coldbox.system" = { levelMin="FATAL", levelMax="INFO", appenders="*" },
		"model.security" = { levelMax="DEBUG", appenders="console" }
	}
	// Implicit categories
	debug = [ "coldbox.system.interceptors"  ],
	info  = [ "model.class", "model2.class2" ],
	warn  = [ "model.class", "model2.class2" ],
	error = [ "model.class", "model2.class2" ],
	fatal = [ "model.class", "model2.class2" ],
	off   = [ "model.class", "model2.class2" ]
};
```

## Instantiation

Once you have defined the configuration data in this object you can now use the same LogBox Config object to either instantiate it for you or you can pass a reference of it by using the `init()` method of the `LogBoxConfig` object:

```javascript
init([CFCConfig,CFCConfigPath])
```

* `CFCConfig` : The object instance that has the logbox configuration data
* `CFCConfigPath` : The instantiation path of the object that has the logbox configuration data

```javascript
// Using config path
config = createObject( "component", "logbox.system.logging.config.LogBoxConfig" )
    .init( CFCConfigPath="my.path.LogBoxConfig" );
logBox = createObject( "component", "logbox.system.logging.LogBox" ).init( config );

// Using config object
data = createObject( "component", "my.data.CFC" );
config = createObject( "component", "logbox.system.logging.config.LogBoxConfig" ).init( data );
logBox = createObject( "component", "logbox.system.logging.LogBox" ).init( config );
```

That's it! Using this DSL approach, your configurations are much more portable now and can even be shared in ANY framework, ColdBox or ColdFusion application. So now let's explore how to bypass this data CFC and use the `LogBoxConfig` object directly. It is important to understand these methods as they are called for you when you define your LogBox DSL data.
