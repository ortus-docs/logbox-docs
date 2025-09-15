# Configuring LogBox

LogBox comes pre-configured for operation with very basic logging.  However, you can customize it to your fancy using different configuration strategies using the programmatic configuration object or the [LogBox Config DSL](logbox-dsl.md).

When you are in a ColdBox application, you will have a `logbox` structure in your `ColdBox.cfc` already that you can use, or you can create a portable CFC as well and place it in `config/LogBox.cfc`

{% hint style="success" %}
The cool thing about this LogBox DSL is that it is the same whether you are using LogBox in ColdBox applications or any other framework or non-framework ColdFusion application.&#x20;
{% endhint %}

Configuration can be done in the following ways:

1. **No configuration:** Uses the _default configuration_ shown below
2. **Portable CFC:** Creating a portable data CFC using the LogBox DSL in a `configure()` method
3. **LogBoxConfig:** Creating the `LogBoxConfig` object and interacting with its methods programmatically
4. **LogBox DSL Struct:** Passing a struct literal into LogBox, using the LogBox DSL.

{% content-ref url="logbox-dsl.md" %}
[logbox-dsl.md](logbox-dsl.md)
{% endcontent-ref %}

### 1. Default Configuration

This is the default configuration when LogBox is created with no config:

{% code lineNumbers="true" %}
```cfscript
component {

  /**
   *  Configure logBox
   */
  function configure(){
    logBox = {
	// Define Appenders
	appenders : { 
		console : { class : "ConsoleAppender" } 
	},
	
	// Root Logger
	root : { 
		levelmax : "INFO", 
		appenders : "*" 
	}
    };
  }

}

// Instantiate it
application.logbox = new logbox.system.logging.LogBox();
```
{% endcode %}



### 2. Portable CFC

You can create a CFC with a single `configure` method with the LogBox configuration in a variable called `logbox` using the LogBox DSL.

```cfscript
component output="false" hint="A LogBox Configuration Data Object" {

/**
 * Configure LogBox, that's it!
 */
function configure(){
    logBox = {
	// Define Appenders
	appenders : {
		coldboxTracer : {
			class      : "ConsoleAppender",
			layout     : "coldbox.tests.specs.logging.MockLayout",
			properties : { name : "awesome" }
		}
	},
	// Root Logger
	root       : { levelmax : "INFO", levelMin : 0, appenders : "*" },
	// Categories
	categories : {
		"coldbox.system"              : { levelMax : "INFO" },
		"coldbox.system.interceptors" : { levelMin : 0, levelMax : "DEBUG", appenders : "*" },
		"hello.model"                 : { levelMax : 4, appenders : "*" }
	},
	debug : [ "coldbox.system", "models.system" ],
	info  : [ "hello.model", "yes.wow.wow" ],
	warn  : [ "hello.model", "yes.wow.wow" ],
	error : [ "hello.model", "yes.wow.wow" ],
	fatal : [ "hello.model", "yes.wow.wow" ],
	OFF   : [ "hello.model", "yes.wow.wow" ]
    };
}

}


// Instantiate it by passing the path to this CFC
application.logbox = new logbox.system.logging.LogBox( "config.LogBoxConfig" );
```



### 3. Programmatic LogBoxConfig

```cfscript
config = new logbox.system.logging.config.LogBoxConfig();

// Appenders
config
  .appender( name = "luis", class = "coldbox.system.logging.appenders.ConsoleAppender" )
  .appender( name = "luis2", class = "coldbox.system.logging.appenders.ConsoleAppender" )
  .root( appenders = "luis,luis2" )
  // Sample categories
  .OFF( "coldbox.system" )
  .debug( "coldbox.system.async" );

// init logBox with Config CFC
application.logbox = new logbox.system.logging.LogBox( config );
```



### 4. Struct Literal Config

```cfscript
var logBox = new logbox.system.logging.LogBox(
   {
	appenders : { myConsoleLiteral : { class : "ConsoleAppender" } },
	root      : { levelmax : "FATAL", appenders : "*" },
	info      : [ "hello.model", "yes.wow.wow" ],
	warn      : [ "hello.model", "yes.wow.wow" ],
	error     : [ "hello.model", "yes.wow.wow" ]
   }
);
```
