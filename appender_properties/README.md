# Appender Properties

As we mentioned before, LogBox ships with over 10 different appenders for your logging and tracing needs. Some of them require configuration properties and some don't. We already discovered that when we configure an appender we can pass in a structure of properties much like how we configure ColdBox Interceptors. Each appender can implement as many properties as they see fit. We will digest all the included LogBox appenders and their configuration properties.

## Async Property
All appenders have an `async` boolean property by default inherited from LogBox.  This will tell LogBox to log asynchronously in a separate thread.  By default all logging is done **synchronously**