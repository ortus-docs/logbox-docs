# Security Levels

LogBox defines six logging levels as numeric constants. Levels control which messages each logger and appender processes — the lower the number, the more severe the message.

| Constant | Value | Description |
| -------- | ----- | ----------- |
| `OFF`    | `-1`  | Logging disabled. No messages are processed. |
| `FATAL`  | `0`   | Critical errors that cause application failure. |
| `ERROR`  | `1`   | Runtime errors and unexpected conditions. |
| `WARN`   | `2`   | Potentially harmful situations that are not errors. |
| `INFO`   | `3`   | General informational messages about application flow. |
| `DEBUG`  | `4`   | Fine-grained diagnostic messages for developers. |

## Using Level Constants

The `this.logLevels` reference on every Logger and Appender exposes the level constants so you never need to hard-code numeric values.

{% tabs %}
{% tab title="BoxLang" %}
```java
// Get a logger bound to this component
var log = logBox.getLogger( this )

// Log only when the level is active (avoids string construction)
if ( log.canDebug() ) {
    log.debug( "Entering processOrder" )
}

// Use named constants when configuring level ranges
var levelMin = log.logLevels.WARN   // 2
var levelMax = log.logLevels.FATAL  // 0
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
// Get a logger bound to this component
var log = logBox.getLogger( this );

// Log only when the level is active (avoids string construction)
if ( log.canDebug() ) {
    log.debug( "Entering processOrder" );
}

// Use named constants when configuring level ranges
var levelMin = log.logLevels.WARN;   // 2
var levelMax = log.logLevels.FATAL;  // 0
```
{% endtab %}
{% endtabs %}

## LogLevels Utility Methods

The `LogLevels` class (`logbox.system.logging.LogLevels`) provides utilities for working with levels programmatically. Both Logger and Appender expose this object via `this.logLevels`.

| Method | Description |
| ------ | ----------- |
| `string lookup( numeric level )` | Returns the English name for a numeric level. e.g. `2` → `"WARN"`. |
| `numeric lookupAsInt( string level )` | Returns the numeric value for an English level name. e.g. `"WARN"` → `2`. Returns `999` if not found. |
| `string lookupCF( numeric level )` | Returns the CFML-compatible severity string for use with `cflog`. e.g. `1` → `"Error"`, `3` → `"Information"`. |
| `boolean isLevelValid( numeric level )` | Returns `true` if the level is within the valid range `-1` to `4`. |

## Level Ranges in Configuration

Appenders accept both numeric values and English names for `levelMin` and `levelMax`:

```javascript
appenders : {
    errorOnly : {
        class    : "FileAppender",
        levelMin : "FATAL",   // 0 — most severe
        levelMax : "ERROR"    // 1
    },
    verbose : {
        class    : "ConsoleAppender",
        levelMin : 0,         // FATAL
        levelMax : 4          // DEBUG — log everything
    }
}
```

{% hint style="info" %}
When `levelMin` and `levelMax` are omitted from an appender definition, LogBox defaults to `FATAL` (0) and `DEBUG` (4), meaning the appender processes all severity levels.
{% endhint %}
