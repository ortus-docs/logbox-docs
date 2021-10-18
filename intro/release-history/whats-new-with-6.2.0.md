# What's New With 6.2.0

LogBox 6.2.0 is a minor release with some bug fixes and some new nice features.

## Release Notes

{% tabs %}
{% tab title="LogBox" %}
### Bugs

* \[[LOGBOX-56](https://ortussolutions.atlassian.net/browse/LOGBOX-56)] - Missing line break on file appender control string

### New Features

* \[[LOGBOX-57](https://ortussolutions.atlassian.net/browse/LOGBOX-57)] - new `shutdown() `method to process graceful shutdown of LogBox
* \[[LOGBOX-58](https://ortussolutions.atlassian.net/browse/LOGBOX-58)] - New logbox config `onShutdown()` callback, which is called when LogBox has been shutdown
* \[[LOGBOX-59](https://ortussolutions.atlassian.net/browse/LOGBOX-59)] - New `shutdown() `method can be now used in appenders that will be called when LogBox is shutdown
{% endtab %}
{% endtabs %}
