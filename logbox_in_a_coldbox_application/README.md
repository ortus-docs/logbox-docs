# LogBox in a ColdBox Application

Every ColdBox application can use LogBox by default since the main engine already uses it. By default ANY ColdBox application will be configured with a LogBox instance with the following appenders:

* ConsoleAppender

```javascript
<LogBox>
	<-- <Default Appender Definitions -->
	<Appender name="ConsoleAppender"  class="coldbox.system.logging.appenders.ConsoleAppender" />

	<-- <Root Logger: Will log anything by default -->
	<Root levelMin="FATAL" levelMax="INFO" appenders="*" />

</LogBox>
```
Also, the app will log on ANY severity by default up to <i>INFO</i> for the root logger and the ColdBox package. You can customize this default behavior by creating or modifying the <i>&lt;LogBox&gt;</i> element in your ColdBox configuration file and follow the same configuration approach as any normal LogBox configuration file; please refer to the configuring LogBox section. In ColdBox 3.0.0 applications and above you can either use the XML or configuration DSL approach.
