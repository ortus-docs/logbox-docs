# Creating a Custom Layout

You can easily create a custom layout object by creating a cfc that extends our abstract layout object: `logbox.system.logging.Layout` and implementing a `format()` method. Below you can see the method signature:

```javascript
<!--- format --->
<cffunction name="format" output="false" access="public" returntype="string" hint="Format a logging event message into your own format">
    <cfargument name="logEvent" type="logbox.system.logging.LogEvent" required="true" hint="The logging event to use to create a message.">
</cffunction>
```

All you need to do is inspect the logging event and create your very own message and then return it back. That's it! You thought there was more?

To configure LogBox to use your custom layout object, set the `layout` key in your LogBox configuration with the dotted component path to your custom layout object. See [Appenders in the Configuration section](https://logbox.ortusbooks.com/configuration/configuring-logbox/logbox-dsl#appenders)
