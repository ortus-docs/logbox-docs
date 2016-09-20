# Adding Categories Granularly

You can also add categories with very granular information using the category() method. This method will allow you to add a category definition with a range of severity levels and even a list of which appenders to respond to.

```js
public void category(
    string name,
    [numeric levelMin='0',]
    [numeric levelMax='4',]
    [string appenders='*']
)
```

Parameters:

* `name` - A unique name for the appender to register. Only unique names can be registered per instance.
* `levelMin` - The default min log level for this category. Defaults to the lowest level 0 or FATAL
* `levelMax` - The max default log level for this category. If not passed it defaults to the highest level possible
* `appenders` - A list of appender names to configure this category with else it will use all the appenders in the root logger. You can also use * to add all registered apenders.

```javascript
//log all email service messages to the MyLogFileAppender and the Console.
config.category(name="org.model.EmailService",appenders="MyLogFileAppender,Console");
```


