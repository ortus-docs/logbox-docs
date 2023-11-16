# LogBox DSL

As we have seen the LogBox DSL can be used in different contexts:

* Portable CFC with a `configure()` method in a `logbox` variable
* ColdBox config inside the `configure()` method in a `logbox` variable
* A struct literal sent in to the constructor of LogBox

NO matter how you dice it, it's the same LogBox Config DSL:

```cfscript
**
* A LogBox configuration data object
*/
component{

    function configure(){
        logBox = {
            
            appenders : {},
            
            root : {},
            
            categories : {},
            
            fatal : [],
            error : [],
            warn  : [],
            info  : [],
            debug : [],
            off   : []

        };
    }
}
```

## Base Config

Root level configuration keys.

<table data-header-hidden><thead><tr><th width="224">Key</th><th>Description</th></tr></thead><tbody><tr><td>Key</td><td>Description</td></tr><tr><td><code>appenders</code></td><td>A structure where you will define appenders</td></tr><tr><td><code>root</code></td><td>A structure where you will configure the root logger</td></tr><tr><td><code>categories</code></td><td>A structure where you can define granular categories (OPTIONAL)</td></tr><tr><td><code>DEBUG</code></td><td>An array that will hold all the category names to place under the DEBUG logging level (OPTIONAL)</td></tr><tr><td><code>INFO</code></td><td>An array that will hold all the category names to place under the INFO logging level (OPTIONAL)</td></tr><tr><td><code>WARN</code></td><td>An array that will hold all the category names to place under the WARN logging level (OPTIONAL)</td></tr><tr><td><code>ERROR</code></td><td>An array that will hold all the category names to place under the ERROR logging level (OPTIONAL)</td></tr><tr><td><code>FATAL</code></td><td>An array that will hold all the category names to place under the FATAL logging level (OPTIONAL)</td></tr><tr><td><code>OFF</code></td><td>An array that will hold all the category names to not log at all (OPTIONAL)</td></tr></tbody></table>

### Appenders

<pre class="language-javascript"><code class="lang-javascript">appenders : {

    console: { class : "ConsoleAppender" },
    
    <a data-footnote-ref href="#user-content-fn-1">jsonConsole</a> : {
        class : "ConsoleAppender",
        layout : "models.JSONLayout",
        levelMin : 0,
        levelMax : 4
    },
    
    errorLog: { 
        class: "FileAppender",
        properties: {
            filePath : "/logs",
            fileName : "appname-errors"     
        },
        levelMin : "FATAL",
        levelMax : "ERROR"
    }
}
</code></pre>

To define an appender you must define a struct with a key value which is the internal name of the appender. Each appender's name must be unique. You configure each appender with the following keys:

| Key          | Description                                                                                   |
| ------------ | --------------------------------------------------------------------------------------------- |
| `class`      | The class path of the appender                                                                |
| `properties` | The properties struct for the appender (OPTIONAL)                                             |
| `layout`     | The layout class path of the layout object to use (OPTIONAL)                                  |
| `levelMin`   | The numerical or English word of the minimal logging level (OPTIONAL, defaults to 0 \[FATAL]) |
| `levelMax`   | The numerical or English word of the maximum logging level (OPTIONAL, defaults to 4 \[DEBUG]) |

### Root Logger

To configure the root logger, use the following keys:

```javascript
root : {
    levelMax : "INFO",
    appenders : "*"
}

root : {
    appenders : "console",
    levelMax : "DEBUG"
}
```

<table data-header-hidden><thead><tr><th width="148">Key</th><th>Description</th></tr></thead><tbody><tr><td>Key</td><td>Description</td></tr><tr><td><code>levelMin</code></td><td>The numerical or English word of the minimal logging level (OPTIONAL, defaults to 0 [FATAL])</td></tr><tr><td><code>levelMax</code></td><td>The numerical or English word of the maximum logging level (OPTIONAL, defaults to 4 [DEBUG])</td></tr><tr><td><code>appenders</code></td><td>A string list of the appenders to use for logging  or the <code>*</code> convention for all appenders.</td></tr></tbody></table>

### Categories

```cfscript
// Granualr Categories
categories={
    "coldbox.system" = { levelMin="FATAL", levelMax="INFO", appenders="*" },
    "model.security" = { levelMax="DEBUG", appenders="console" }
}
```

To define categories, you define a struct with a key value, which is the internal name of the category. **Each category name must be unique**,. You configure each category with the following keys:

<table data-header-hidden><thead><tr><th width="152">Key</th><th>Description</th></tr></thead><tbody><tr><td>Key</td><td>Description</td></tr><tr><td><code>levelMin</code></td><td>The numerical or English word of the minimal logging level (OPTIONAL, defaults to 0 [FATAL])</td></tr><tr><td><code>levelMax</code></td><td>The numerical or English word of the maximum logging level (OPTIONAL, defaults to 4 [DEBUG])</td></tr><tr><td><code>appenders</code></td><td>A string list of the appenders to use for logging (OPTIONAL, defaults to *)</td></tr></tbody></table>

As you might notice, the names of the keys on all the structures match 100% to the programmatic methods you can also use to configure logBox. So, when in doubt, refer back to the argument names.

#### Example Configuration

```javascript
logBox = {
    // Appenders
    appenders = {
        appenderName = {
            class="class.to.appender",
            layout="class.to.layout",
            levelMin=0,
            levelMax=4,
            properties={
                name  = value,
                prop2 = value 2
            }
    },
    // Root Logger
    root = { levelMin="FATAL", levelMax="DEBUG", appenders="*" },
    // Granualr Categories
    categories={
        "coldbox.system" = { levelMin="FATAL", levelMax="INFO", appenders="*" },
        "model.security" = { levelMax="DEBUG", appenders="console" }
    }
    // Implicit categories
    debug = [ "coldbox.system.interceptors"  ],
    info  = [ "model.class", "model2.class2" ],
    warn  = [ "model.class", "model2.class2" ],
    error = [ "model.class", "model2.class2" ],
    fatal = [ "model.class", "model2.class2" ],
    off   = [ "model.class", "model2.class2" ]
};
```



[^1]: 
