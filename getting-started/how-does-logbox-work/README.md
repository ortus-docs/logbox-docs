# How Does LogBox Work?

![](<../../.gitbook/assets/image (3).png>)

LogBox has five main components:

1. **LogBox**
   1. The central library that stores your loggers, appenders, categories, and configuration
2. **Logger**
   1. The class in charge of sending messages to the appropriate destinations according to the category it has been defined with.
3. **Categories**
   1. Each Logger is created with a unique category that usually maps to the classpath of the CFC that uses the logger.
4. **Appenders**
   1. Components that receive log events and send them for storage in their implementations: files, consoles, etc.
5. **Layouts**
   1. The appenders will send the messages to their destinations using a specified format.  This is called the layout of the message. LogBox comes with default layouts, but you can build your own.

These components work in unison to deliver messages' logging and tracing and control how they are logged. You will primarily interact with the **Logger** component as it will send your statements to the **Appenders** you have configured. Users can extend LogBox and build custom appenders and layouts.
