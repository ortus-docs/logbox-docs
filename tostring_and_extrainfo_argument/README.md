# $toString() and ExtraInfo Argument

When using any of the logging methods like <i>info(),debug(),warn()</i>, etc, they all take two arguments: 1) The message to log and 2) An extraInfo argument which can be anything you like. This extra info argument can be a simple value, a CFC, a complex object and pretty much anything you like. The appenders get this extra info argument and they can process it into their appropriate destinations by serializing its value to simple form. This is done by using the following algorithm:

1. If it is a simple value, then just use it
2. If it is an object then check if the object has a method called <i>$toString()</i>
    1. If the method exists, then call <i>$toString()</i> and use its return value
2. If it is an object with NO $toString() then marshall its representation in XML format
3. If it is a complex variable like a struct, query, array, etc, then marshall it to JSON format

As you can see from the algorithm above, you can use the extra info argument to your benefit to save serialized representations of data to the appenders and then retrieve or re-inflate them later. The $toString() convention is great because you have complete control on how a CFC will serialize to its string representation. Let's see an example on a simple CFC:

```javascript
component{

	function $toString(){
		// return my representation as a comma list of values of my properties
		return "#getName()#,#getAge()#,#getEmail()#";
	}
}
```

So when this object is sent to a logger's method, it will detect it is an object and the $toString() function exists and call it for serialization.

```javascript
user = userService.getUser(rc.id);

// need to log it.
if( log.canDebug() ){
	log.debug("User just got logged in right now!", user);
}
```


