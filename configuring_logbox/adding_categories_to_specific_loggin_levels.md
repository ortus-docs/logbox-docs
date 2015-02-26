# Adding Categories to Specific Loggin Levels
The methods shown below are used to add categories to specific severity levels only. Each method can receive 1 to* category arguments.

* <i>public void DEBUG()</i>
* <i>public void INFO()</i>
* <i>public void WARN()</i>
* <i>public void ERROR()</i>
* <i>public void FATAL()</i>
* <i>public void OFF()</i>

```javascript
config.debug("com.model.myclass", "coldbox.system.controller");
config.info("com.model.otherclass", "coldbox.system.whatever");
config.fatal("com.model.otherclass", "coldbox.system.whatever");
config.error("com.model.otherclass", "coldbox.system.whatever");
config.OFF("com.model.otherclass", "coldbox.system.whatever");
```


