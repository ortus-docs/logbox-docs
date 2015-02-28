# Configuring The Root Logger
This is also mandatory if you will be using LogBox, you must add a root logger configuration. This is very easy and few arguments.

```js
public void root([numeric levelMin='-1'], [numeric levelMax='4'], string appenders)
```

Parameters:
* `levelMin` - The default log level for the root logger, by default it is 0. Optional.
* `levelMax` - The default log level for the root logger, by default it is 4. Optional.
* `appenders` - A list of appenders to configure the root logger with. Use * to add all registered appenders


```javascript
config.root(appenders="*");
config.root(levelMax=config.logLevels.WARN,appenders="console,files");
config.root(levelMin=config.logLevels.INFO,levelMax=config.logLevels.DEBUG,appenders="*");
```
