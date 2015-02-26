# Dealing With Custom Layouts

In order for an appender to deal with custom layouts, you must use the layout methods when preparing to log your messages. Below is a simple example from the console appender of how to do this:

```javascript
if( hasCustomLayout() ){
  entry = getCustomLayout().format(loge);
}
else{
  entry = "#severityToString(loge.getseverity())# #loge.getCategory()# #loge.getmessage()# ExtraInfo: #loge.getextraInfoAsString()#";
}

// Log message to system.out
instance.out.println(entry);
```

As you can see, all you need to do is have an if statement that checks whether the appender has a custom layout or not and then assign the return of the layout as your message to log.
