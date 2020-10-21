# Table of contents

* [Introduction](README.md)

## Intro

* [Release History](intro/release-history/README.md)
  * [What's New With 6.1.0](intro/release-history/whats-new-with-6.1.0.md)
  * [What's New With 6.0.0](intro/release-history/whats-new-with-6.0.0.md)
* [About This Book](intro/about-this-book.md)
* [Author](intro/author.md)

## Getting Started

* [Features at a Glance](getting-started/features-at-a-glance.md)
* [Installation](getting-started/installation/README.md)
  * [LogBox Refcard](getting-started/installation/logbox-refcard.md)
* [Need For Logging](getting-started/need-for-logging.md)
* [How Does LogBox Work?](getting-started/how-does-logbox-work/README.md)
  * [LogBox](getting-started/how-does-logbox-work/logbox.md)
  * [Appender](getting-started/how-does-logbox-work/appender.md)
  * [Logger](getting-started/how-does-logbox-work/logger/README.md)
    * [Logger Category Inheritance](getting-started/how-does-logbox-work/logger/logger-category-inheritance.md)
    * [Security Levels](getting-started/how-does-logbox-work/logger/security-levels.md)
    * [Dynamic Appenders](getting-started/how-does-logbox-work/logger/dynamic-appenders.md)
  * [Layout](getting-started/how-does-logbox-work/layout.md)

## Configuration

* [Configuring LogBox](configuration/configuring-logbox/README.md)
  * [LogBox DSL](configuration/configuring-logbox/logbox-dsl.md)
  * [Adding Appenders](configuration/configuring-logbox/adding-appenders.md)
  * [Adding Categories to Specific Loggin Levels](configuration/configuring-logbox/adding-categories-to-specific-loggin-levels.md)
  * [Adding Categories Granularly](configuration/configuring-logbox/adding-categories-granularly.md)
  * [Configuring The Root Logger](configuration/configuring-logbox/configuring-the-root-logger.md)

## Usage

* [Using LogBox](usage/using-logbox.md)
* [Using a Logger Object](usage/using-a-logger-object/README.md)
  * [Can Methods For Performance](usage/using-a-logger-object/can-methods-for-performance.md)
  * [$toString\(\) and ExtraInfo Argument](usage/using-a-logger-object/usdtostring-and-extrainfo-argument.md)
* [Appender Properties](usage/appender-properties/README.md)
  * [CFAppender](usage/appender-properties/cfappender.md)
  * [ConsoleAppender](usage/appender-properties/consoleappender.md)
  * [DBAppender](usage/appender-properties/dbappender.md)
  * [EmailAppender](usage/appender-properties/emailappender.md)
  * [FileAppender](usage/appender-properties/fileappender.md)
  * [RollingFileAppender](usage/appender-properties/rollingfileappender.md)
  * [ScopeAppender](usage/appender-properties/scopeappender.md)
  * [SocketAppender](usage/appender-properties/socketappender.md)
  * [TraceAppender](usage/appender-properties/traceappender.md)
* [LogBox in a ColdBox Application](usage/logbox-in-a-coldbox-application/README.md)
  * [Configuration Within ColdBox](usage/logbox-in-a-coldbox-application/configuration-within-coldbox.md)
  * [Benefits of using LogBox in a ColdBox application](usage/logbox-in-a-coldbox-application/benefits-of-using-logbox-in-a-coldbox-application.md)
  * [Where is LogBox stored in a ColdBox app?](usage/logbox-in-a-coldbox-application/where-is-logbox-stored-in-a-coldbox-app.md)
  * [LogBox from the ColdBox Proxy](usage/logbox-in-a-coldbox-application/logbox-from-the-coldbox-proxy.md)
  * [The LogBox Injection DSL](usage/logbox-in-a-coldbox-application/the-logbox-injection-dsl.md)

## Extending LogBox

* [Creating Custom  Appenders](extending-logbox/creating-custom-appenders/README.md)
  * [Helper Methods](extending-logbox/creating-custom-appenders/helper-methods.md)
  * [Instance Members](extending-logbox/creating-custom-appenders/instance-members.md)
  * [Dealing With Custom Layouts](extending-logbox/creating-custom-appenders/dealing-with-custom-layouts.md)
  * [Registering Appenders at Runtime](extending-logbox/creating-custom-appenders/registering-appenders-at-runtime.md)
* [Creating a Custom Layout](extending-logbox/creating-a-custom-layout/README.md)
  * [Instance Members](extending-logbox/creating-a-custom-layout/instance-members.md)

