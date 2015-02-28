# Helper Methods

The abstract appender also has various cool methods that you can use when building appenders:

##Properties Methods

* `truct getProperties()` : Get all the properties struct
* `void setProperties(struct properties)` : Override all properties
* `any getProperty(string property)` : Get a property
* `void setProperty(string property, any value)` : Set a property
* `Boolean propertyExists(string property)` : Checks if a property exists

## Utility Methods
* `isInitialized()` : If the appender has been initialized
* `getName()` : Get the name of the appender
* `getHash()` : Get the appender's unique hash id
* `severityToString(numeric severity)` : Transforms a severity integer to it's human readable form

## Layout Methods
* `any getCustomLayout()` : Get the custom layout object if defined.
* `boolean hasCustomLayout()` : Checks if the custom layout object is defined in this appender.





