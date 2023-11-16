# Configuring LogBox

No matter what configuration you decide to use, you will always have to instantiate LogBox with a `LogBoxConfig` object: `logbox.system.logging.config.LogBoxConfig`. However, you can either talk directly to this CFC or create a more portable configuration. We denote This portable configuration as a simple data CFC that contains the LogBox configuration data using our **LogBox DSL** (Domain Specific Language).

{% hint style="success" %}
The cool thing about this LogBox DSL is that it is the same whether you are using LogBox in ColdBox applications or any other framework or non-framework ColdFusion application.&#x20;
{% endhint %}

Configuration can be done in the following ways

1. No configuration uses the _default configuration_ shown below
2. Creating a portable data CFC using the LogBox DSL
3. Creating the `LogBoxConfig` object and interacting with its methods programmatically

### Default Configuration

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
```
{% endcode %}
