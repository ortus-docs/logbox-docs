# DBAppender

| Property   | Type    | Required | Default | Description                                                          |
| ---------- | ------- | -------- | ------- | -------------------------------------------------------------------- |
| dsn        | string  | true     | ---     | The dsn to use for logging                                           |
| table      | string  | true     | ---     | The table name to use for logging                                    |
| columnMap  | struct  | false    | ---     | A column map for aliasing columns. (Optional)                        |
| autocreate | boolean | false    | false   | if true, then we will create the table. Defaults to false (Optional) |

The columns needed or created in the table are

* `id` : UUID
* `severity` : string
* `category` : string
* `logdate` : timestamp
* `appendername` : string
* `message` : string
* `extrainfo` : string

If you are building a column mapper, the map must have the above keys in it that match to your own table columns.
