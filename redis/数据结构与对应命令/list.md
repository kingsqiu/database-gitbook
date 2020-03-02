# 列表

## 命令

**基本命令**

| 命令     | 用例和描述                                                   |
| -------- | ------------------------------------------------------------ |
| `RPUSH`  | `RPUSH` `key-name` `value` `[value...]`<br /> 将一个或多个值推入列表的右端 |
| `LPUSH`  | `LPUSH` `key-name` `value` `[value...]`<br />将一个或多个值推入列表的左端 |
| `RPOP`   | `RPOP` `key-name` <br />移除并返回列表最右端的元素           |
| `LPOP`   | `LPOP` `key-name` <br />移除并返回列表最左端的元素           |
| `LINDEX` | `LINDEX` `key-name` `offset` <br />返回列表中偏移量为offset的元素 |
| `LRANGE` | `LRANGE` `key-name` `start` `end`<br /> 返回列表从start偏移量到end偏移量范围内的所有元素，其中偏移量为start和偏移量为end的元素也会包含在被返回的元素之内 |
| `LTRIM`  | `LTRIM` `key-name` `start` `end` <br />对列表进行修剪，只保留从`start`漂移量到`end`偏移量范围内的元素，其中偏移量为`start`和偏移量为`end`的元素也会被保留。 |

**阻塞式的列表弹出命令以及在列表之间移动元素的命令**

| 命令         | 用例和描述                                                   |
| ------------ | ------------------------------------------------------------ |
| `BLPOP`      | `BLPOP` `key-name` `[key-name...]` `timeout`<br />从第一个非空列表中弹出位于最左端的元素，或者在`timeout`秒之内阻塞并等待可弹出的元素出现 |
| `BRPOP`      | `BRPOP` `key-name` `[key-name...]` `timeout`<br />从第一个非空列表中弹出位于最右端的元素，或者在`timeout`秒之内阻塞并等待可弹出的元素出现 |
| `RPOPLPUSH`  | `RPOPLPUSH` `source-key` `dest-key` <br />从`source-key`列表中弹出位于最右端的元素，然后将这个元素推入`dest-key`列表的最左端，并向用户返回这个元素 |
| `BRPOPLPUSH` | `BRPOPLPUSH` `souce-key` `dest-key` `timeout` <br />从`source-key`列表中弹出位于最右端的元素，然后将这个元素推入`dest-key` 列表的最左端，并向用户返回这个元素；如果`source-key`为空，那么在`timeout`秒之内阻塞并等待可弹出的元素出现。 |



