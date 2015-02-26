# EmailAppender
|Property|Type|Required|Default|Description|
|--|--|--|--|
|subject|string |true |---|Get's pre-pended with the severity and category field. |
|from|string |true |--- |The from email address |
|to |string|true|---|The to email(s) |
|cc |string|false |empty |The cc email(s) |
|bcc |string|false|empty |The bcc email(s) |
|mailserver |string|false |empty |The optional mail server |
|mailusername |string|false |empty |The optional mail username |
|mailpassword |string|false |empty |The optional mail password |
|mailport |int|false |25|The optional mail port |
|useTLS |boolean |false |false |Use the Transport level security setting in the cfmail tag. |
|useSSL |boolean |false|false|Use SSL or not|

