# Where is LogBox stored in a ColdBox app?

The LogBox instance is stored in the ColdBox main controller object (`coldbox.system.web.Controller`) and you can retrieve it like so from any handler,  or interceptor.

```javascript
logBox = getController().getLogBox();
// or 
logBox
```

## WireBox Injection

WireBox is also configured to allow an injection DSL for logBox:

```
// Inject LogBox
inject="logbox"

// Inject the root logger
inject="logbox:root"

// Inject a named category logger
inject="logbox:logger:category"

// Inject a logger using the instance's path as the category
inject="lobox:logger:{this}
```
