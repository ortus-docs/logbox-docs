# Adding Categories to Specific Logging Levels
The methods shown below are used to add categories to specific severity levels only. Each method can receive 1 to * category arguments.

* `public void DEBUG()`
* `public void INFO()`
* `public void WARN()`
* `public void ERROR()`
* `public void FATAL()`
* `public void OFF()`

```javascript
config.debug("com.model.myclass", "coldbox.system.controller");
config.info("com.model.otherclass", "coldbox.system.whatever");
config.fatal("com.model.otherclass", "coldbox.system.whatever");
config.error("com.model.otherclass", "coldbox.system.whatever");
config.OFF("com.model.otherclass", "coldbox.system.whatever");
```


