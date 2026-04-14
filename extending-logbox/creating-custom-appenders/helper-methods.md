# Helper Methods

The abstract appender also has various cool methods that you can use when building appenders:

## Properties Methods

| Method                                         | Description                                           |
| ---------------------------------------------- | ----------------------------------------------------- |
| `struct getProperties()`                       | Get the entire properties struct.                     |
| `void setProperties(struct properties)`        | Override all properties with a new properties struct. |
| `any getProperty(string property)`             | Get a property.                                       |
| `void setProperty(string property, any value)` | Set a property.                                       |
| `boolean propertyExists(string property)`      | Checks if a property exists.                          |

## Utility Methods

| Method                                      | Description                                               |
| ------------------------------------------- | --------------------------------------------------------- |
| `boolean isInitialized()`                   | Returns true if the appender has been initialized.        |
| `string getName()`                          | Get the name of the appender                              |
| `string getHash()`                          | Get the appender's unique hash id                         |
| `string severityToString(numeric severity)` | Transforms a severity integer to it's human readable form |

## Layout Methods

| Method                      | Description                                                     |
| --------------------------- | --------------------------------------------------------------- |
| `any getCustomLayout()`     | Get the custom layout object if defined.                        |
| `boolean hasCustomLayout()` | Checks if the custom layout object is defined in this appender. |

## Level Methods

| Method | Description |
| ------ | ----------- |
| `boolean canLog( numeric level )` | Returns `true` if the given numeric level falls within this appender's configured `levelMin`–`levelMax` range. Use this to short-circuit expensive log preparation before calling `logMessage()`. |

## Output and Locking Helpers

These private helpers are available inside your appender implementation:

| Method | Description |
| ------ | ----------- |
| `lock( required body, type = "exclusive" )` | Executes the passed closure/lambda under a named CFML lock scoped to this appender's hash and name. `type` may be `"exclusive"` (default) or `"readonly"`. Honors the `lockTimeout` property. |
| `out( required message )` | Writes a message to the JVM **standard output** stream (`System.out`). Useful for diagnostic output during appender development. |
| `err( required message )` | Writes a message to the JVM **standard error** stream (`System.err`). Useful for surfacing low-level appender errors without triggering further logging. |
