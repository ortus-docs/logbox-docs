# Configuration Within ColdBox

There are several ways you can configure LogBox from within your ColdBox applications, to each its own. So we will start with the two ways you can configure a ColdBox application.

### Programmatic
ColdBox 3.0.0 and above allows for a programmatic approach via the ColdBox configuration object. So let's look at how the loader looks at your configuration:

* Is there a logBox variable defined in the configuration?
    * False:
        * Does a LogBox.cfc <i>exist in the application's config folder</i>?
            * True: Use that CFC by convention to configure LogBox
            * False: Continue to next point
        * Configure LogBox with default framework settings
    * True:
        * Have you defined a <i>configFile</i> key?
            * True: Then use that value to pass into the configuration object so it can load LogBox using that configuration file (xml or CFC)
            * False: The configuration data is going to be defined inline here so process it

So the configuration DSL is exactly the same as you have seen in before with the only distinction that you can add a configFile key that can point to an external configuration file (XML or CFC).

<br>

#### XML
The XML approach uses exactly the same configuration elements as the normal XML configuration file but with one extra element: ConfigFile. This serves the same purpose as in the programmatic approach, where you have defined the LogBox configuration somewhere and you are pointing to it via this setting:

```javascript
<LogBox>
	<ConfigFile>shared.path.LogBoxConfig</ConfigFile>
</LogBox>
```

Please also note that the application loader follows almost the same approach as above:

* Is there a &lt;logBox&gt; element defined in the configuration?
    * False:
        * Does a LogBox.cfc <i>exist in the application's config folder</i>?
            * True: Use that CFC by convention to configure LogBox
            * False: Continue to next point
        * Configure LogBox with default framework settings
    * True:
        * Have you defined a &lt;configFile&gt; element?
            * True: Then use that value to pass into the configuration object so it can load LogBox using that configuration file (xml or CFC)
            * False: The configuration data is going to be defined inline here so process it
