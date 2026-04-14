# Async Appenders

`AbstractAppender` includes a built-in **async queue system** that lets your custom appender accept log events on the calling thread and ship them to their destination in a background scheduled task. This is ideal for I/O-heavy appenders (databases, sockets, HTTP endpoints) where synchronous logging would block the application.

## How It Works

1. Your `logMessage()` implementation calls `queueMessage( data )` instead of writing directly.
2. `queueMessage()` appends the payload to an in-memory array and calls `startLogListener()`.
3. `startLogListener()` lazily schedules a `runLogListener()` task via the ColdBox Task Scheduler (double-lock safe).
4. The task drains the queue — calling your `processQueueElement()` override for each item — until the queue is empty and has been idle for a configurable period.
5. On application shutdown, LogBox calls `shutdown()` with a synchronous force-flush so no messages are lost.

## Enabling Async Logging

Set a property named `async` in your appender's `properties` struct and check it inside `logMessage()` to decide whether to queue or write directly:

{% tabs %}
{% tab title="BoxLang" %}
```java
class extends="logbox.system.logging.AbstractAppender" {

    function logMessage( required logEvent ){
        var entry = buildEntry( logEvent )

        if ( getProperty( "async", false ) ) {
            // Non-blocking: hand off to the queue
            queueMessage( entry )
        } else {
            // Blocking: write directly
            writeEntry( entry )
        }
    }

    // Called by the async listener for each queued item
    function processQueueElement( required data, required queueContext, required queue ){
        writeEntry( data )
    }

    private function writeEntry( required entry ){
        // ... write to your destination
    }

    private function buildEntry( required logEvent ){
        return {
            severity  : severityToString( logEvent.getSeverity() ),
            message   : logEvent.getMessage(),
            category  : logEvent.getCategory(),
            timestamp : logEvent.getTimestamp(),
            extraInfo : logEvent.getExtraInfo()
        }
    }

}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
component extends="logbox.system.logging.AbstractAppender" {

    function logMessage( required logEvent ){
        var entry = buildEntry( logEvent );

        if ( getProperty( "async", false ) ) {
            // Non-blocking: hand off to the queue
            queueMessage( entry );
        } else {
            // Blocking: write directly
            writeEntry( entry );
        }
    }

    // Called by the async listener for each queued item
    function processQueueElement( required data, required queueContext, required queue ){
        writeEntry( data );
    }

    private function writeEntry( required entry ){
        // ... write to your destination
    }

    private function buildEntry( required logEvent ){
        return {
            severity  : severityToString( logEvent.getSeverity() ),
            message   : logEvent.getMessage(),
            category  : logEvent.getCategory(),
            timestamp : logEvent.getTimestamp(),
            extraInfo : logEvent.getExtraInfo()
        };
    }

}
```
{% endtab %}
{% endtabs %}

Configure it in the LogBox DSL:

```javascript
appenders : {
    myCustom : {
        class      : "models.logging.MyAppender",
        properties : { async : true }
    }
}
```

## Queue API Reference

### `queueMessage( required data )`

Appends `data` (any struct or value) to the internal queue array and ensures the log-listener task is running. Returns `this` (fluent). This call is **non-blocking**.

### `startLogListener()`

Lazily starts the background log-listener scheduled task. Called automatically by `queueMessage()`. Uses a double-check lock so only one task runs per appender at a time.

### `runLogListener( force = false )`

The scheduled task entry point. Drains the queue by repeatedly calling `processQueueElement()` until the queue is empty and has been idle for `maxIdle` milliseconds (default 10 000 ms). When `force = true` (called synchronously during shutdown) it processes all remaining items without sleeping.

## Lifecycle Hook Methods

Override any of these no-op stubs in your appender to react to queue processing events. Each receives a `queueContext` struct:

```javascript
queueContext = {
    lastRun       : // getTickCount() of last processed item
    start         : // getTickCount() when listener started
    maxIdle       : // 10000 ms — listener shuts down after this idle period
    sleepInterval : // 25 ms — nap between empty-queue checks
    count         : // number of elements processed so far
    force         : // true when called from shutdown
}
```

| Method | When It Fires |
| ------ | ------------- |
| `onLogListenerStart( queueContext )` | Once, when the listener task begins. Good for opening connections or allocating resources. |
| `onLogListenerSleep( queueContext )` | Each iteration before the listener sleeps (queue is empty, waiting for more messages). |
| `onLogListenerEnd( queueContext )` | Once, when the listener task exits (queue drained and idle timeout reached). Good for flushing buffers or closing connections. |
| `preProcessQueue( queue, queueContext )` | Before each queue-drain iteration. Receives the live queue array. |
| `postProcessQueue( queue, queueContext )` | After each queue-drain iteration. Receives the live queue array. |
| `processQueueElement( data, queueContext, queue )` | For each item popped from the queue. **Override this** to deliver the payload to your destination. |

## Batching Example

Use `preProcessQueue` / `postProcessQueue` to batch multiple items into a single write:

{% tabs %}
{% tab title="BoxLang" %}
```java
function onLogListenerStart( required struct queueContext ){
    queueContext.batch = []
}

function preProcessQueue( required queue, required struct queueContext ){
    // drain the full queue into the batch before processing
    while ( queue.len() ) {
        queueContext.batch.append( queue.first() )
        queue.deleteAt( 1 )
    }
}

function processQueueElement( required data, required struct queueContext, required queue ){
    // no-op: all items already moved to batch
}

function postProcessQueue( required queue, required struct queueContext ){
    if ( queueContext.batch.len() ) {
        writeBatchToDestination( queueContext.batch )
        queueContext.batch = []
    }
}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
function onLogListenerStart( required struct queueContext ){
    queueContext.batch = [];
}

function preProcessQueue( required queue, required struct queueContext ){
    // drain the full queue into the batch before processing
    while ( queue.len() ) {
        queueContext.batch.append( queue.first() );
        queue.deleteAt( 1 );
    }
}

function processQueueElement( required data, required struct queueContext, required queue ){
    // no-op: all items already moved to batch
}

function postProcessQueue( required queue, required struct queueContext ){
    if ( queueContext.batch.len() ) {
        writeBatchToDestination( queueContext.batch );
        queueContext.batch = [];
    }
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
The queue array is a plain CFML/BoxLang array and is **not thread-safe** on its own. The built-in `lock()` helper wraps access to the queue in a named lock automatically. If you access `variables.logListener.queue` directly, wrap the call in `lock()`.
{% endhint %}
