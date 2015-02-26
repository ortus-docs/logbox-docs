# Security Levels
Each logger will be configured with an optional severity level range: LevelMin and LevelMax. These severities are integers from -1 to 4, each representing a severity:

|Severity|Integer Level|
|--|--|
|OFF|-1|
|FATAL|0 (Default LevelMin) |
|ERROR |1|
|WARN |2|
|INFO|3|
|DEBUG|4 (Default LevelMax)|

As you can see from the chart above the default minimum level is FATAL (all messages are ignored except fatal, uncaught errors) and the highest level is DEBUG (debug listens and logs all messages). When you define a root logger or category logger you should define them using a severity level from the table above. If you do not define a severity level a default level will be used. Once you have a logger instantiated you can dynamically change the logging levels by interacting with the setLevelMin() and setLevelMax() methods of the logger you have instantiated.

```javascript
//change min level of logging to warn only
logger = logBox.getRootLogger();
logger.setLevelMin(logger.logLevels.WARN);
```

Each logger object has a public property called logLevels that maps to the component: coldbox.system.loggging.LogLevels which is used as a static lookup of severity levels. You may use the alias, or, the numeric level; however, it is best practice to use a level alias (such as DEBUG or INFO).

