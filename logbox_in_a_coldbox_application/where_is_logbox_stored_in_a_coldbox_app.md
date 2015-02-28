# Where is LogBox stored in a ColdBox app?

The LogBox instance is stored in the ColdBox main controller object (`coldbox.system.web.Controller`) and you can retrieve it like so from any handler,  or interceptor.

```javascript
logBox = getController().getLogBox();
// or 
logBox
```