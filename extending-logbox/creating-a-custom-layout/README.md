# Creating a Custom Layout

You can easily create a custom layout object by creating a class that extends `logbox.system.logging.Layout` and implementing a `format()` method. Below you can see the method signature:

{% tabs %}
{% tab title="BoxLang" %}
```java
class extends="logbox.system.logging.Layout" {

    string function format( required logbox.system.logging.LogEvent logEvent ){
        // inspect logEvent and return your formatted string
        return "[#logEvent.getSeverity()#] #logEvent.getCategory()# - #logEvent.getMessage()#"
    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component extends="logbox.system.logging.Layout" {

    string function format( required logbox.system.logging.LogEvent logEvent ){
        // inspect logEvent and return your formatted string
        return "[#logEvent.getSeverity()#] #logEvent.getCategory()# - #logEvent.getMessage()#";
    }

}
```
{% endtab %}
{% endtabs %}

All you need to do is inspect the logging event, build your message string, and return it. That's it!

To configure LogBox to use your custom layout object, set the `layout` key in your LogBox configuration with the dotted class path to your custom layout object. See [Appenders in the Configuration section](https://logbox.ortusbooks.com/configuration/configuring-logbox/logbox-dsl#appenders)
