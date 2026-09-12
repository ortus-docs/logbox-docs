# DBAppender

| Property     | Type    | Required | Default | Description                                                                              |
| ------------ | ------- | -------- | ------- | ---------------------------------------------------------------------------------------- |
| dsn          | string  | true     | ---     | The dsn to use for logging                                                               |
| table        | string  | true     | ---     | The table name to use for logging                                                        |
| schema       | string  | false    | ---     | The schema the table lives in. When set, the table is referenced as `schema.table`. (Optional) |
| columnMap    | struct  | false    | ---     | A column map for aliasing columns. (Optional)                                            |
| autocreate   | boolean | false    | false   | if true, then we will create the table. Defaults to false (Optional)                     |
| ensureChecks | boolean | false    | true    | If true, verifies (and auto-creates, if `autocreate` is true) the table on appender registration. Set to false to skip these checks. (Optional) |
| defaultCategory | string | false | The appender's `name` | The category value stored when the log event has no category. (Optional)              |
| rotate       | boolean | false    | true    | If true, delete records older than `rotationDays`. Defaults to true (Optional)           |
| rotationDays | integer | false    | 30      | If `rotate` is true, delete records older than `rotationDays`. Defaults to 30 (Optional) |
| rotationFrequency | integer | false | 5   | If `rotate` is true, the number of minutes to wait between rotation checks. Defaults to 5 (Optional) |

The columns needed or created in the table are

* `id` : UUID
* `severity` : string
* `category` : string
* `logdate` : timestamp
* `appendername` : string
* `message` : string
* `extrainfo` : string

If you are building a column mapper, the map must have the above keys in it that match to your own table columns.
