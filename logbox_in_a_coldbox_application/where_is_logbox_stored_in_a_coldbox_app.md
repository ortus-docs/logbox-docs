# Where is LogBox stored in a ColdBox app?

The LogBox instance is stored in the ColdBox main controller object and you can retrieve it like so from any handler, plugin or interceptor.

```javascript
logBox = getController().getLogBox();
```

