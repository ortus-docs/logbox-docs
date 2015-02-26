# Helper Methods

The abstract appender also has various cool methods that you can use when building appenders:

CF Utility Methods

* <i>$abort()</i>
* <i>$abort()</i>
* <i>$log(string severity='INFO', string message=) : Log a cflog message just in case</i>
* <i>$rethrowit(any throwObject)</i>
* <i>$throw(string message, [string detail=], [string type='Framework'])</i>


Properties Methods

*  <i>truct getProperties()</i> : Get all the properties struct
*  <i>void setProperties(struct properties)</i> : Override all properties
*  <i>any getProperty(string property)</i> : Get a property
*  <i>void setProperty(string property, any value)</i> : Set a property
*  <i>Boolean propertyExists(string property)</i> : Checks if a property exists

Utility Methods
* <i>isInitialized()</i> : If the appender has been initialized
* <i>getName()</i> : Get the name of the appender
* <i>getHash()</i> : Get the appender's unique hash id
* <i>severityToString(numeric severity)</i> : Transforms a severity integer to it's human readable form

Layout Methods
* <i>any getCustomLayout()</i> : Get the custom layout object if defined.
* <i>boolean hasCustomLayout()</i> : Checks if the custom layout object is defined in this appender.





