# LogBox in a ColdBox Application

Every ColdBox application can use LogBox by default since the main engine already uses it. By default ANY ColdBox application will be configured with a LogBox instance with the following appenders:

```javascript
component{

    function configure(){
        logBox = {};

        // Define Appenders
        logBox.appenders = {
            console = { class="coldbox.system.logging.appenders.DummyAppender" }
        };

        // Root Logger
        logBox.root = {
            levelmax="OFF",
            levelMin="OFF",
            appenders="*"
        };
    }

}
```

Also, the app will log on **ANY** severity by default up to `INFO` for the root logger and the ColdBox package. You can customize this default behavior by creating or modifying the `LogBox` element in your ColdBox configuration file and follow the same configuration approach as any normal LogBox configuration file.

