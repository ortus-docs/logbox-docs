# Registering Appenders at Runtime

You can programmatically register appenders at runtime by using the registerAppender() function exposed in the LogBox object. Here is the function API:

```javascript
registerAppender(name, class, properties, layout, levelMin, levelMax);
```

> <b>Information</b> Please note that registering dynamic appenders at runtime is tricky as some objecs might already have references to some appenders. We recommend registering appenders at configuration load or when the application starts up.
