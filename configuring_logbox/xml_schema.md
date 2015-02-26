# XML Schema

We have also included a schema fileL <i>coldbox/logging/config/LogBoxConfig.xsd</i> that you can use to validate your XML and use cool tag insight and introspection. You can add the following header to your XML declaration file to enable it:

```javascript
<?xml version="1.0" encoding="UTF-8"?>
<LogBox xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:noNamespaceSchemaLocation="http://www.coldbox.org/schema/LogBoxConfig_1.4.xsd">

</LogBox>
```

If your IDE supports XML introspection, this will do the trick.
