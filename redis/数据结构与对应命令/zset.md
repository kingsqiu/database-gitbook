# 有序集合

## 命令

常用简单命令

| 命令      | 用例和描述                                                   |
| --------- | ------------------------------------------------------------ |
| `ZADD`    | `ZADD` `key-name` `score` `member` `[score member ...]`<br />将带有给定分值的成员添加到有序集合里面 |
| `ZREM`    | `ZREM` `key-name` `member` `[member ...]`<br />从有序集合里面移除给定的成员，并返回被移除成员的数量 |
| `ZCARD`   | `ZCARD` `key-name`<br />返回有序集合包含的成员数量           |
| `ZINCRBY` | `ZINCRBY` `key-name` `increment` `member` <br />将`member`成员的分值加上`increment` |
| `ZCOUNT`  | `ZCOUNT` `key-name` `min` `max` <br />返回分值介于`min`和`max`之间的成员数量 |
| `ZRANK`   | `ZRANK` `key-name` `member` <br />返回成员`member`在有序集合中的排名 |
| `ZSCORE`  | `ZSCORE` `key-name` `member` <br />返回成员`member`的分值    |
| `ZRANGE`  | `ZRANGE` `key-name` `start` `stop` `[WITHSCORES]`<br />返回有序集合中排名介于`start`和`stop`之间的成员，如果给定了可选的`WITHSCORES`选项，那么命令会将成员的分值也一并返回。 |

有序集合的范围型数据获取命令和范围型数据删除命令，以及并集命令和交集命令

| 命令               | 用例和描述 |
| ------------------ | ---------- |
| `ZREVRANK`         |            |
| `ZREVRANGE`        |            |
| `ZTANGEBYSCORE`    |            |
| `ZREVRANGEBYSCORE` |            |
| `ZREMRANGEBYRANK`  |            |
| `ZREMRANGEBYSCORE` |            |
| `ZINTERSTORE`      |            |
| `ZUNIONSTORE`      |            |



## 介绍

## 备注

## 疑问