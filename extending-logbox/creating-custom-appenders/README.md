# Creating Custom Appenders

In order to create your own appenders, you will have to create a cfc that extends `logbox.system.logging.AbstractAppender` and implement the following methods:

| Method               | Description                                                                                                                        |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `init()`             | Your constructor. Make sure to call `super.init( argumentCollection=arguments );`                                                  |
| `logMessage()`       | The method that is called when a message is received.                                                                              |
| `onRegistration()`   | An interceptor that fires when the appender gets created and initialized. It can be used for preparing the appender for operation. |
| `onUnRegistration()` | An interceptor that fires when the appender is removed from a logger.                                                              |

## `init()`

The signature of the init method is the following:

{% tabs %}
{% tab title="BoxLang" %}
```java
function init(
    required name,
    struct properties = {},
    layout            = "",
    levelMin          = 0,
    levelMax          = 4
){
    super.init( argumentCollection = arguments )
    // your setup here
    return this
}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
function init(
    required name,
    struct properties = {},
    layout            = "",
    numeric levelMin  = 0,
    numeric levelMax  = 4
){
    super.init( argumentCollection = arguments );
    // your setup here
    return this;
}
```
{% endtab %}
{% endtabs %}

As you can see each appender receives a `name`, a structure of `properties`, an optional `layout` class, and optional `levelMin` and `levelMax` severity levels. The `properties` and `layout` are both optional, but you must call `super.init( argumentCollection = arguments )` to have full appender operation. Here is a `FileAppender`-style example:

{% tabs %}
{% tab title="BoxLang" %}
```java
function init(
    required name,
    struct properties = {},
    layout            = "",
    levelMin          = 0,
    levelMax          = 4
){
    super.init( argumentCollection = arguments )

    if ( !propertyExists( "filepath" ) ) {
        throw( message = "Filepath property not defined", type = "FileAppender.PropertyNotFound" )
    }
    if ( !propertyExists( "autoExpand" ) )   { setProperty( "autoExpand", true ) }
    if ( !propertyExists( "filename" ) )     { setProperty( "filename", getName() ) }
    if ( !propertyExists( "fileEncoding" ) ) { setProperty( "fileEncoding", "UTF-8" ) }

    var filePath = getProperty( "filePath" ).reReplace( "[/\\]$", "" )
    variables.logFullPath = filePath & "/" & getProperty( "filename" ) & ".log"
    if ( getProperty( "autoExpand" ) ) {
        variables.logFullPath = expandPath( variables.logFullPath )
    }

    return this
}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
function init(
    required name,
    struct properties = {},
    layout            = "",
    numeric levelMin  = 0,
    numeric levelMax  = 4
){
    super.init( argumentCollection = arguments );

    if ( !propertyExists( "filepath" ) ) {
        throw( message = "Filepath property not defined", type = "FileAppender.PropertyNotFound" );
    }
    if ( !propertyExists( "autoExpand" ) )   { setProperty( "autoExpand", true ); }
    if ( !propertyExists( "filename" ) )     { setProperty( "filename", getName() ); }
    if ( !propertyExists( "fileEncoding" ) ) { setProperty( "fileEncoding", "UTF-8" ); }

    var filePath = reReplaceNoCase( getProperty( "filePath" ), "[/\\]$", "" );
    variables.logFullPath = filePath & "/" & getProperty( "filename" ) & ".log";
    if ( getProperty( "autoExpand" ) ) {
        variables.logFullPath = expandPath( variables.logFullPath );
    }

    return this;
}
```
{% endtab %}
{% endtabs %}

## `logMessage()`

The signature of the `logMessage` method is the following:

{% tabs %}
{% tab title="BoxLang" %}
```java
function logMessage( required logbox.system.logging.LogEvent logEvent ){
    // write to your destination
}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
function logMessage( required logbox.system.logging.LogEvent logEvent ){
    // write to your destination
}
```
{% endtab %}
{% endtabs %}

As you can see it is a very simple method that receives a LogBox logging event object. This object keeps track of the following properties with its appropriate getters and setters:

* `timestamp`
* `category`
* `message`
* `severity`
* `extraInfo`

You can then use this logging event object to log to whatever destination you want. Here is a snippet from a scope appender:

{% tabs %}
{% tab title="BoxLang" %}
```java
function logMessage( required logEvent ){
    var logStack = getStorage()
    var limit    = getProperty( "limit" )
    var loge     = logEvent

    ensureStorage()

    if ( limit > 0 && logStack.len() >= limit ) {
        // pop the oldest entry
        logStack.deleteAt( 1 )
    }

    logStack.append( {
        id          : createUUID(),
        logDate     : loge.getTimestamp(),
        appenderName: getName(),
        severity    : severityToString( loge.getSeverity() ),
        message     : loge.getMessage(),
        extraInfo   : loge.getExtraInfo(),
        category    : loge.getCategory()
    } )

    saveStorage( logStack )
}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
function logMessage( required logEvent ){
    var logStack = getStorage();
    var limit    = getProperty( "limit" );
    var loge     = logEvent;

    ensureStorage();

    if ( limit > 0 && logStack.len() >= limit ) {
        // pop the oldest entry
        logStack.deleteAt( 1 );
    }

    logStack.append( {
        id          : createUUID(),
        logDate     : loge.getTimestamp(),
        appenderName: getName(),
        severity    : severityToString( loge.getSeverity() ),
        message     : loge.getMessage(),
        extraInfo   : loge.getExtraInfo(),
        category    : loge.getCategory()
    } );

    saveStorage( logStack );
}
```
{% endtab %}
{% endtabs %}

## `onRegistration()` & `onUnregistration()`

Both the `onRegistration` and `onUnregistration` methods are void methods with no arguments. They are great for starting or stopping resources. Here is a sample from a socket appender:

{% tabs %}
{% tab title="BoxLang" %}
```java
function onRegistration(){
    if ( getProperty( "persistConnection" ) ) {
        openConnection()
    }
}

function onUnRegistration(){
    if ( getProperty( "persistConnection" ) ) {
        closeConnection()
    }
}
```
{% endtab %}
{% tab title="CFML" %}
```cfscript
function onRegistration(){
    if ( getProperty( "persistConnection" ) ) {
        openConnection();
    }
}

function onUnRegistration(){
    if ( getProperty( "persistConnection" ) ) {
        closeConnection();
    }
}
```
{% endtab %}
{% endtabs %}
