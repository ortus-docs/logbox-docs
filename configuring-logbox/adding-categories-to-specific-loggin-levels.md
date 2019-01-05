# Adding Categories to Specific Logging Levels

The methods shown below are used to add categories to specific severity levels only. Each method can receive 1 to \* category arguments.

* `public void debug()`
* `public void info()`
* `public void warn()`
* `public void error()`
* `public void fatal()`
* `public void off()`

```javascript
config.debug( "com.model.myclass", "coldbox.system.controller" );
config.info( "com.model.otherclass", "coldbox.system.whatever" );
config.fatal( "com.model.otherclass", "coldbox.system.whatever" );
config.error( "com.model.otherclass", "coldbox.system.whatever" );
config.off( "com.model.otherclass", "coldbox.system.whatever" );
```

