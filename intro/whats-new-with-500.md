# What's New With 5.0.0

This is a major release and a major rewrite of the entire framework to modern CFML, optimizations and script modes.  

We have also improved all appenders for performance and reliability. Especially, the file logging facilities have been drastically improved.  The new file based appenders now rely on a queuing mechanism and listener watcher threads that stream content to the file repositories.


## Release Notes
                                
### Improvements

* [<a href='https://ortussolutions.atlassian.net/browse/LOGBOX-16'>LOGBOX-16</a>] - Allow chaining of logger programmatic config methods
* [<a href='https://ortussolutions.atlassian.net/browse/LOGBOX-20'>LOGBOX-20</a>] - FileAppender IO improvements via LogListener Watchers
* [<a href='https://ortussolutions.atlassian.net/browse/LOGBOX-26'>LOGBOX-26</a>] - Add extraInfo to the message before clean-up, to allow for correct csv exports
* [<a href='https://ortussolutions.atlassian.net/browse/LOGBOX-28'>LOGBOX-28</a>] - Console Appender sent error messages to error out