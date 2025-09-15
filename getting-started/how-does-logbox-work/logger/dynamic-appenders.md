# Dynamic Appenders

Each logger object has several methods that you can use in order to interact with the logger's appenders. You can add, remove, clear or list the appenders on a specific logger instance. Below are the methods you can use in the logger class to interact with appenders:

| Method                | Return Type | Description                                               |
| --------------------- | ----------- | --------------------------------------------------------- |
| hasAppenders()        | `Boolean`   | Checks if the logger has any appenders attached to it     |
| getAppenders()        | `Struct`    | Returns the map of registered appenders                   |
| getAppender(name)     | `Appender`  | Return a named appender if it is registered in the logger |
| appenderExists(name)  | `Boolean`   | Checks if a named appender exists in the logger           |
| addAppender(Appender) | `void`      | Register an appender with the logger at runtime           |
| removeAppender(name)  | `Boolean`   | Will un-register an appender from this logger             |
| removeAllAppenders()  | `void`      | Will try to un-register all appenders from this logger    |

So you can easily add/remove/check the appenders on any logger at any time.

```javascript
//Add your own appender at runtime
jms = createObject( "component", "com.appender.JMSAppender" ).init( "JMSAppender", properties );
logger.addAppender( jms );

//log a message to all appenders and to my jms appender:
logger.fatal( "I FAILED MAN!" );

//remove it
logger.removeAppender( "JMSAppender" );
```
