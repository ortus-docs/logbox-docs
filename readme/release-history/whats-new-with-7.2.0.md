---
description: November 18, 2023
---

# What's New With 7.2.0

You can read all about this release on our main What's New Page: [https://coldbox.ortusbooks.com/readme/release-history/whats-new-with-7.2.0](https://coldbox.ortusbooks.com/readme/release-history/whats-new-with-7.2.0)

### Release Notes

The full release notes per library can be found below. Just click on the library tab and explore their release notes:

{% tabs %}
{% tab title="LogBox" %}
#### New Feature

[LOGBOX-75](https://ortussolutions.atlassian.net/browse/LOGBOX-75) New listeners for all appenders: preProcessQueue() postProcessQueue()

[LOGBOX-76](https://ortussolutions.atlassian.net/browse/LOGBOX-76) Add the queue as an argument to the processQueueElement() method

[LOGBOX-79](https://ortussolutions.atlassian.net/browse/LOGBOX-79) new rolling appender property archiveLayout which is a closure that returns the pattern of the archive layout

#### Bug

[LOGBOX-73](https://ortussolutions.atlassian.net/browse/LOGBOX-73) Unhandled race conditions in FileRotator lead to errors and potential log data loss

[LOGBOX-77](https://ortussolutions.atlassian.net/browse/LOGBOX-77) log rotator was not checking for file existence and 1000s of errors could be produced

#### Improvement

[LOGBOX-62](https://ortussolutions.atlassian.net/browse/LOGBOX-62) Support ad-hoc struct literal of LogBox DSL to configure LogBox

[LOGBOX-70](https://ortussolutions.atlassian.net/browse/LOGBOX-70) Add \`Exclude\` key to Logbox Categories to Easily Exclude Appenders

[LOGBOX-74](https://ortussolutions.atlassian.net/browse/LOGBOX-74) shutdown the appenders first instead of the executors to avoid chicken and egg issues

[LOGBOX-78](https://ortussolutions.atlassian.net/browse/LOGBOX-78) Change fileMaxArchives default from 2 to 10

#### Task

[LOGBOX-72](https://ortussolutions.atlassian.net/browse/LOGBOX-72) Removal of instance approach in preferences to accessors for the LogBoxConfig
{% endtab %}
{% endtabs %}
