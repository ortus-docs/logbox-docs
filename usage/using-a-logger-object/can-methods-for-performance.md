# When To Log

We recommend using the available `can{severity}()` methods or a closure message approach to determine if we can log at a specific log level before writing the logging method line. This is done as best practice to avoid processing messages that will never be logged anyway.&#x20;

### Less Performant

So let's look at a very simple example of what **NOT** to do:

```javascript
log.debug( "This is my log message, some #dynamic# date is here", dataCFC );
```

This will call the logger's `debug()` method, execute the lines of code, and then the logger determines if it can be logged.&#x20;

### Can{} Methods

This is okay, but we all love performance and best practice, so we encourage you to do the following:

```javascript
if( log.canDebug() ){
    log.debug( "This is my log message, some #dynamic# date is here", dataCFC );
}
```

This way, the logger determines if it can send debug log messages and only **if it can**.

### Closure Wrapper

You can also avoid the if statements by using a closure as the message. This will ONLY execute it if the logging level is available for logging.

```cfscript
log.debug( () => "This is my log message, some #dynamic# date is here", dataCFC );
```
