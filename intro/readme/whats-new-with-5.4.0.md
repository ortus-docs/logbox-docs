# What's New With 5.4.0

## Improvements

There are two major improvements we did with LogBox in this release:

1\) The file locking operations on file appenders have been streamlined to avoid high i/o operations.

2\) The console appender uses an asynchronous streaming technique which makes it extremely efficient and fast.

## Release Notes

### New Feature

* \[[LOGBOX-34](https://ortussolutions.atlassian.net/browse/LOGBOX-34)\] - Console appender completely rewritten to support asynchronous streaming

### Improvement

* \[[LOGBOX-33](https://ortussolutions.atlassian.net/browse/LOGBOX-33)\] - Improve file exists usage on file appenders to avoid i/o operations

