# The LogBox Injection DSL

The ColdBox autowiring DSL can also talk to LogBox. This way you can easily use our dependency injection DSL for LogBox related objects:

|Type|Description|
|--|--|
|logbox |Get a reference to the application's LogBox instance |
|logbox:root |Get a reference to the root logger |
|logbox:logger:category |Get a reference to a named logger by its category name|
|logbox:logger:{this} |Get a reference to a named logger according to the current class path of the injected target|

Below you can see the most common usage of this dependency DSL:

```javascript
<---  LogBox wired in --->
<cfproperty name="logBox" type="logbox" />

<---  Root Logger --->
<cfproperty name="logger" type="logbox:root" />


<---  Named Category For an Object, will grab the category name from the object itself. --->
<cfproperty name="logger" type="logbox:logger:#getMetadata(this).name#" />

<---  Named Category --->
<cfproperty name="logger" type="logbox:logger:com.api.model" />

<---  Category eq to ClassPath --->
<cfproperty name="logger" type="logbox:logger:{this}" />
```
