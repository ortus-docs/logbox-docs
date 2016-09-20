# Using LogBox

Once you have created and configured the LogBox library, you can interact with it in order to get logger objects. The main methods you will use to interact with LogBox are the following, but I recommend you look at the CFC api ([http://www.coldbox.org/api](http://www.coldbox.org/api)) in order to get a listing of all available methods.

* `LogBoxConfig getConfig()` : Get the config object registered
* `Logger getLogger(any category)` : Get a named logger object using a category string or the object you will log from
* `Logger getRootLogger()` : Get a reference to the root logger
* `string getVersion()` : Get the current version of LogBox
* `string getCurrentAppenders()` : Get a list of currently registered appenders
* `string getCurrentLoggers()` : Get a list of currently instantiated loggers
* `void configure( LogBoxConfig config )` : Dynamically re-configure the LogBox library

The two most important methods are `getRootLogger() & getLogger()`, which you will use to get the root or named logger objects.

> **Caution:** When you ask for a named category logger and LogBox cannot find its definition, it will create a logger that will inherit its logging levels and appenders from the root logger.


