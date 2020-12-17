# Configuring The Root Logger

Configuring a root logger is mandatory for LogBox. This is very easy and just a few arguments.

```javascript
public void root([numeric levelMin="-1",] [numeric levelMax="4",] string appenders)
```

## Parameters

| Name | Description |
| :--- | :--- |
| levelMin | The default minimum log level for the root logger. \(OPTIONAL. Defaults to 0 \[FATAL\].\) |
| levelMax | The default maximum log level for the root logger. \(OPTIONAL. Defaults to 4 \[DEBUG\].\) |
| appenders | A list of appenders to configure the root logger with. Use `*` to add all registered appenders |

```javascript
config.root( appenders="*" );
config.root( levelMax="WARN", appenders="console,files" );
config.root( levelMin="INFO", levelMax="DEBUG", appenders="*" );
```

