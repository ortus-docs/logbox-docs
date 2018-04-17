# Helper Methods

The abstract appender also has various cool methods that you can use when building appenders:

## Properties Methods

| Method | Description |
| --- | --- |
| `struct getProperties()` | Get the entire properties struct. |
| `void setProperties(struct properties)` | Override all properties with a new properties struct. |
| `any getProperty(string property)` | Get a property. |
| `void setProperty(string property, any value)` | Set a property. |
| `boolean propertyExists(string property)` | Checks if a property exists. |

## Utility Methods

| Method | Description |
| --- | --- |
| `boolean isInitialized()` | Returns true if the appender has been initialized. |
| `string getName()` | Get the name of the appender |
| `string getHash()` | Get the appender's unique hash id |
| `string severityToString(numeric severity)` | Transforms a severity integer to it's human readable form |

## Layout Methods

| Method | Description |
| --- | --- |
| `any getCustomLayout()` | Get the custom layout object if defined. |
| `boolean hasCustomLayout()` | Checks if the custom layout object is defined in this appender. |

