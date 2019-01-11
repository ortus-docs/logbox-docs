# What's New With 5.0.0

This is a major release and a major rewrite of the entire framework to modern CFML, optimizations and script modes.

We have also improved all appenders for performance and reliability. Especially, the file logging facilities have been drastically improved. The new file based appenders now rely on a queuing mechanism and listener watcher threads that stream content to the file repositories.

## Release Notes

### Improvements

* \[[LOGBOX-16](https://ortussolutions.atlassian.net/browse/LOGBOX-16)\] - Allow chaining of logger programmatic config methods
* \[[LOGBOX-20](https://ortussolutions.atlassian.net/browse/LOGBOX-20)\] - FileAppender IO improvements via LogListener Watchers
* \[[LOGBOX-26](https://ortussolutions.atlassian.net/browse/LOGBOX-26)\] - Add extraInfo to the message before clean-up, to allow for correct csv exports
* \[[LOGBOX-28](https://ortussolutions.atlassian.net/browse/LOGBOX-28)\] - Console Appender sent error messages to error out

