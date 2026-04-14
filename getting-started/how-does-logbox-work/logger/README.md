# Logger

A **Logger** is the primary object you interact with to emit log messages. Each Logger is bound to a **category name** — typically the full component path — and inherits its configuration (appenders and log levels) from LogBox's category hierarchy.

## Getting a Logger

Obtain a Logger from the `LogBox` instance:

{% tabs %}
{% tab title="BoxLang" %}
```java
// By object reference — uses the full component path as the category name
var log = logBox.getLogger( this )

// By explicit category string
var log = logBox.getLogger( "com.myapp.services.UserService" )

// Root logger — receives everything not matched by a named category
var log = logBox.getRootLogger()
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
// By object reference — uses the full component path as the category name
var log = logBox.getLogger( this );

// By explicit category string
var log = logBox.getLogger( "com.myapp.services.UserService" );

// Root logger — receives everything not matched by a named category
var log = logBox.getRootLogger();
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
When LogBox cannot find a named category definition, it creates a logger that inherits levels and appenders from the root logger automatically.
{% endhint %}

## Logging Methods

Every Logger exposes a dedicated method for each severity level plus a generic `logMessage()` method:

| Method | Severity | Description |
| ------ | -------- | ----------- |
| `fatal( message, [extraInfo] )` | FATAL (0) | Log a critical failure. |
| `error( message, [extraInfo] )` | ERROR (1) | Log a runtime error. |
| `warn( message, [extraInfo] )` | WARN (2) | Log a potential problem. |
| `info( message, [extraInfo] )` | INFO (3) | Log informational output. |
| `debug( message, [extraInfo] )` | DEBUG (4) | Log diagnostic details. |
| `logMessage( message, severity, [extraInfo] )` | Any | Log at an explicit numeric severity level. |

### Closure Messages (Lazy Evaluation)

Pass a closure as the `message` argument to defer string construction until LogBox confirms the level is active. This avoids unnecessary work when the severity is filtered out:

{% tabs %}
{% tab title="BoxLang" %}
```java
log.debug( () => "Processing #items.len()# items: #items.toList()#" )
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
log.debug( function(){ return "Processing #items.len()# items: #items.toList()#"; } );
```
{% endtab %}
{% endtabs %}

## Sub-Pages

* [Logger Category Inheritance](logger-category-inheritance.md)
* [Security Levels](security-levels.md)
* [Dynamic Appenders](dynamic-appenders.md)
