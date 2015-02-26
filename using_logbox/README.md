# Using LogBox

Once you have created and configured the LogBox library, you can interact with it in order to get logger objects. The main methods you will use to interact with LogBox are the following, but I recommend you look at the CFC api ([http://www.coldbox.org/api](http://www.coldbox.org/api)) in order to get a listing of all available methods.

* <i>LogBoxConfig getConfig()</i> : Get the config object registered
* <i>Logger getLogger(any category)</i> : Get a named logger object using a category string or the object you will log from
* <i>Logger getRootLogger()</i> : Get a reference to the root logger
* <i>string getVersion()</i> : Get the current version of LogBox
* <i>string getCurrentAppenders()</i> : Get a list of currently registered appenders
* <i>string getCurrentLoggers()</i> : Get a list of currently instantiated loggers
* <i>void configure(LogBoxConfig config)</i> : Dynamically re-configure the LogBox library

The two most important methods are <i>getRootLogger() & getLogger()</i>, which you will use to get the root or named logger objects.

> <b>Important</b> When you ask for a named category logger and LogBox cannot find its definition, it will create a logger that will inherit its logging levels and appenders from the root logger.


