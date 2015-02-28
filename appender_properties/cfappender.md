# CFAppender

|Property|Type|Required|Default|Description|
|--|--|--|--|--|
|logType |string(file or application) |false |file |The type of cflog to use: file or application. |
|fileName |string |false |Appender's name |The name of the file to log to if using file as the logType. If not set, it will use the appender's name |

This appender logs directly to the `cflog` tag by using a custom file or logging to the application logs.
