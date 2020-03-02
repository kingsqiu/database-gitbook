# 集合

## 命令

基本命令

| 命令          | 用例和描述                                                   |
| ------------- | ------------------------------------------------------------ |
| `SADD`        | `SADD` `key-name` `item` `[item ...]`<br />将一个或多个元素添加到集合里面，并返回被移除元素的数量 |
| `SREM`        | `SREM` `key-name` `item` `[item ...]`<br />从集合里面移除一个或多个元素，并返回被移除元素的数量 |
| `SISMEMBER`   | `SISMEMBER` `key-name` `item` <br />检查元素item是否存在于集合`key-name`里 |
| `SCARD`       | `SCARD` `key-name` <br />返回集合包含的元素的数量            |
| `SMEMBERS`    | `SMEMBERS` `key-name` <br />返回集合包含的所有元素           |
| `SRANDMEMBER` | `SRANDMEMBER` `key-name` `[count]`<br />从集合里面随机地返回一个或多个元素。当`count`为正数时，命令返回的随机元素不会重复；当`count`为负数时，命令返回的随机元素可能会出现重复 |
| `SPOP`        | `SPOP` `key-name` <br />随机地移除集合中的一个元素，并返回被移除的元素 |
| `SMOVE`       | `SMOVE` `source-key` `dest-key` `item`<br />如果集合`source-key` 包含元素`item`,那么从集合`source-key`里面移除元素`item`,并将元素`item`添加到集合`dest-key`中；如果`item`被成功移除，那么命令返回`1`,否则返回`0` |

组合和处理多个集合的命令

| 命令          | 用例和描述                                                   |
| ------------- | ------------------------------------------------------------ |
| `SDIFF`       | `SDIFF` `key-name` `[key-name ...]`<br />返回那些存在于第一个集合、但不存在于其他集合中的元素（数学上的差集运算） |
| `SDIFFSTORE`  | `SDIFFSTORE` `dest-key` `key-name` `[key-name ...]`<br />将那些存在于第一个集合但并不存在于其他集合中的元素（差集运算）存储到`dest-key`键里面 |
| `SINTER`      | `SINTER` `key-name` `[key-name ...]` <br />返回那些同时存在于所有集合上的元素（数学上的交集运算） |
| `SINTERSTORE` | `SINTERSTORE` `dest-key` `key-name` `[key-name ...]`<br />将那些同时存在于所有集合的元素（交集运算）存储到`dest-key`键里面 |
| `SUNION`      | `SUNION` `key-name` `[key-name ...]`<br />返回那些至少存在于一个集合中的元素（数学上的并集运算） |
| `SUNIONSTORE` | `SUNIONSTORE` `dest-key` `key-name` `[key-name ...]`<br />将那些至少存在于一个集合中的元素（并集运算）存储到`dest-key`键里面 |



## 介绍

## 备注

## 疑问