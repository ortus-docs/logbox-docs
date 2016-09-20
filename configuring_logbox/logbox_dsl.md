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

To define an appender you must define a struct with a key value which is the internal name of the appender.  Each appender name must be unique.  You configure each appender with the following keys:

|Key|Description|
|--|--|
|class|The class path of the appender|
|properties|The properties struct for the appender (OPTIONAL)|
|layout|The layout class path of the layout object to use (OPTIONAL)|
|levelMin|The numerical or English word of the minimal logging level (OPTIONAL, defaults to 0)|
|levelMax|The numerical or English word of the maximum logging level (OPTIONAL, defaults to 4)|

To define the root logger you can use the following keys:

* `levelMin` : The numerical or English word of the minimal logging level (optional, defaults to 0)
* `levelMax` : The numerical or English word of the maximum logging level (optional, defaults to 4)
* `appenders` : A <i>string listof the appenders to use for logging</i>

To define categories you can use the following keys in the categories structure and the key of the structure is the name of the category:

* `levelMin`: The numerical or English word of the minimal logging level (optional, defaults to 0)
* `levelMax`: The numerical or English word of the maximum logging level (optional, defaults to 4)
* `appenders` : A <i>string list of the appenders to use for logging (optional, defaults to *)</i>

As you might notice the name of the keys on all the structures match 100% to the programmatic methods you can also use to configure logBox. So when in doubt, refer back to the argument names.

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
