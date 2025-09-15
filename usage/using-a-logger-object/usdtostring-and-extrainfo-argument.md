# ExtraInfo Serialization

When using any of the logging methods like `info()`, `debug()`, `warn()`, etc, they all take two arguments:

1. The `message` to log as a string or a closure that returns the message
2. An `extraInfo`argument, which can be anything you like.&#x20;

This `extrainfo` argument can be a simple value, a CFC, a complex object, or anything you like. The appenders get this `extraInfo` argument and process it into their appropriate destinations by serializing its value. This is done by using the following algorithm:

1. If it is a simple value, then use it.
2. If it is an object, then check if the object has a method called `$toString()`. If the method exists, then call `$toString()` and use its return value.
3. If it's an exception, marshall it to JSON
4. If it is an object with no `$toString()` method, marshall its representation into XML format.
5. If it is a complex variable like a struct, query, array, etc., then marshall it into JSON format.

### $toString() Convention

As you can see from the algorithm above, you can use the `extraInfo` argument to your benefit to save serialized data representations to the appenders and then retrieve or re-inflate them later. The `$toString()` convention is great because you can control how a CFC will serialize to its string representation. Let's see an example of a simple CFC:

```javascript
// User.cfc
component{

    function $toString(){
        // return my representation as a comma list of values of my properties
        return "#getName()#,#getAge()#,#getEmail()#";
    }
}
```

So when this object is sent to a logger's method, it will detect it is an object, and the `$toString()` function exists and call it for serialization.

```javascript
user = userService.getUser( rc.id );

// need to log it.
if( log.canDebug() ){
    log.debug( "User just got logged in right now!", user );
}
```
