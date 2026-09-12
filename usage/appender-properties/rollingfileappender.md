# RollingFileAppender

| Property        | Type    | Required | Default              | Description                                                                                                                                     |
| --------------- | ------- | -------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| filePath        | string  | true     | ---                  | The location of where to store the log file                                                                                                     |
| filename        | string  | false    | Name of the Appender | The name of the file, if not defined, then it will use the name of this appender. Do not append an extension to it. We will append a .log to it |
| fileEncoding    | string  | false    | utf-8                | The file encoding to use, by default we use UTF-8                                                                                               |
| autoExpand      | boolean | false    | true                 | Whether to expand the file path or not. Defaults to true                                                                                        |
| fileMaxSize     | int     | false    | 2000 (2MB)           | The max file size for log files. Defaults to 2000 (2 MB)                                                                                        |
| fileMaxArchives | int     | false    | 10                   | The max number of archives to keep                                                                                                              |
| archiveLayout   | any     | false    | See below            | A closure/UDF `function( filename, archiveCount )` used to build the archived file's name (without extension) when the log file is rotated      |
| rotatorSchedulerMinutes | numeric | false | 10                | How often (in minutes) the background task checks if the log file needs rotating, after an initial 5 minute delay on registration               |

> **Info** Please remember to set the `autoExpand` property to FALSE if you will be using an absolute file path location.

By default, `archiveLayout` produces archive names in the format `#filename#-#yyyy-MM-dd#-#hh-mm#-#archiveNumber#` (no extension; a `.log` extension is appended automatically). Provide your own closure/UDF to customize the archived file naming convention.
