# Benefits of using LogBox in a ColdBox application

Just by building a ColdBox application, you get several key benefits when dealing with LogBox.

* First of all, the configuration, creation and instantiation is ALL done for you.
* You can configure LogBox on a per-environment criteria as the ColdBox per-environment routines can use the LogBox configuration elements in its definitions.
* Every handler and interceptor already has a reference to the LogBox instance as a property called: `logBox`. So you have immediate access to it.
* Every handler and interceptor already has a configured logger instance as a property called: `log`. So you have immediate access to it.
* You can configure the logging of ColdBox on a per package level.
* You get the power of ColdBox MVC.
