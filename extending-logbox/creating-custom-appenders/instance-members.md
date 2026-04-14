# Instance Members

Every Appender has access to the following public variables and injected references.

## Log Levels Enum

| Property | Description |
| -------- | ----------- |
| `this.logLevels` | A reference to the `logbox.system.logging.LogLevels` class. Use this to access level constants (`this.logLevels.DEBUG`, etc.) and utility methods. |

## Injected References

These variables are automatically set by LogBox when the appender is registered. They are available as `variables.*` inside your appender and are empty strings (`""`) when LogBox is running in standalone mode (outside a ColdBox application).

| Property | Description |
| -------- | ----------- |
| `logBox` | A reference to the running `LogBox` instance. |
| `coldbox` | A reference to the ColdBox application controller. Empty in standalone mode. |
| `wirebox` | A reference to the WireBox injector. Empty in standalone mode. |

## Configuration Properties

| Property | Default | Description |
| -------- | ------- | ----------- |
| `lockTimeout` | `25` | Timeout in seconds used by the base `lock()` helper when acquiring named locks during concurrent appender operations. |
| `logListener` | `{ active: false, queue: [] }` | Internal state for the async queue system. `active` indicates whether the log-listener scheduled task is currently running; `queue` is the array of pending log payloads awaiting processing. See [Async Appenders](async-appenders.md) for details. |
