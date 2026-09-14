# Configuration Within ColdBox

ColdBox allows for a programmatic approach via the `ColdBox.bx` (or `.cfc` for CFML) configuration object. So let's look at how the ColdBox loader looks at your configuration:

1. Is there a `logBox` variable defined in the configuration?
   * **False**:
     * Does a `LogBox.bx` (or `.cfc` for CFML) exist in the application's `config` folder?
       * **True**: Use that class by convention to configure LogBox
       * **False**: Continue to next point
     * Configure LogBox with default framework settings (`coldbox.system.web.config.LogBox`)
   * **True**:
     * Have you defined a `configFile` key?
       * **True**: Then use that value to pass into the configuration object so it can load LogBox using that configuration file (class)
       * **False**: The configuration data is going to be defined inline here so process it

So the configuration DSL is exactly the same as you have seen in before with the only distinction that you can add a `configFile` key that can point to an external configuration file (class).
