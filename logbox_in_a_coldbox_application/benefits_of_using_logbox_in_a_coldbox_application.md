# Benefits of using LogBox in a ColdBox application

Just by building a ColdBox application, you get several key benefits when dealing with LogBox.

* First of all, the configuration, creation and instantiation is ALL done for you.
* The ColdBox configuraiton file accepts ${setting} placeholder syntax, so you can make your LogBox configuration dynamic and use your ColdBox settings. You can even make your properties to appenders to be complex variables as you have the JSON notation available in the ColdBox application already or forget about that nonsense and use the ColdBox Programatic approach.
* You can configure LogBox on a per-environment criteria as the ColdBox per-environment routines can use the LogBox configuration elements in its definitions.
* Every handler, interceptor and plugin already has a reference to the LogBox instance as a property called: logBox. So you have immediate access to it.
* Every handler, interceptor and plugin already has a configured logger instance as a property called: log. So you have immediate access to it.The ColdBox Logger plugin is already configured to use the configured LogBox instance and you can inject it anywhere you like.
* You can configure the logging of ColdBox on a per package level.
* You get the power of ColdBox MVC.


