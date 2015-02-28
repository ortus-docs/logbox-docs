# AsyncRollingFileAppender & RollingFileAppender

|Property|Type|Required|Default|Description|
|--|--|--|--|--|
|filePath|string |true |---|The location of where to store the log file |
|filename |string|false |Name of the Appender |The name of the file, if not defined, then it will use the name of this appender. Do not append an extension to it. We will append a .log to it |
|fileEncoding|string |false |utf-8 |The file encoding to use, by default we use UTF-8 |
|autoExpand |boolean |false |true|Whether to expand the file path or not. Defaults to true |
|fileMaxSize|int|false|2000 (2MB)|The max file size for log files. Defaults to 2000 (2 MB) |
|fileMaxArchives |int|false|2|The max number of archives to keep. Defaults to 2 |

> <b>Info</b> Note: Please remember to set the autoExpand property to FALSE if you will be using an absolute file path location.


