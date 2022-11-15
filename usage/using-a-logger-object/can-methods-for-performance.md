# Can Methods For Performance

We recommend using the available `can{severity}()` methods to determine if we can log at a specific log level before actually writing the logging method line. This is done as best practice in order to avoid processing of messages that will never be logged anyways. So let's look at a very simple example of what **NOT** to do:

```javascript
log.debug( "This is my log message, some #dynamic# date is here", dataCFC );
```

This will call the logger's `debug()` method, execute the lines of code and then the logger determines if it can be logged or not. This is ok, but we all love performance and best practice, so we encourage you to do the following:

```javascript
if( log.canDebug() ){
    log.debug( "This is my log message, some #dynamic# date is here", dataCFC );
}
```

This way, the logger determines if it can send debug log messages, and only **IF IT CAN** does it. This is faster and cleaner, but you will type more. Sorry!
