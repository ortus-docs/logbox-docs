# Features at a Glance

![](../.gitbook/assets/logbox-overview.png)

* LogBox can handle the inserting of logging and/or tracing statements in your application with a simple to use API while providing you the ability to manage logging behavior outside of your application code.
* You can configure LogBox via a programmatic configuration file \(cfc\)
* LogBox categorizes your logging and/or tracing statements according to user-defined categories that can be configured at runtime or pre-runtime. All of these categorizations can have their own logging level ranges \(such as debug or info\) and even their own destination points or what we refer to as LogBox Appenders \(such as Console\).
* LogBox Appenders are the destination points you configure for your logging and/or tracing statements. LogBox also offers a basic extensible API so you can build and extend upon the Appender framework according to your unique logging or tracing needs. This gives you complete control and flexibility of how to expand LogBox without reinventing the wheel. Some appenders included in LogBox can log to the following destinations: File, Database, Sockets, Email, ColdFusion logging, System Console, and much more.
* LogBox facilitates the creation of your very own customized message formats via Layouts. You can create a Layout component that can be configured in to ANY LogBox appender so it can spit out your very own customized messages.
* LogBox can be instantiated as many times as you want and used as many times as you like in a single application. There are no restrictions upon its usage.
* LogBox allows for category inheritance according to component and package conventions.

