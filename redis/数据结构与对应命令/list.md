# 列表

## 命令

基本命令

| 命令     | 用例和描述                                                   |
| -------- | ------------------------------------------------------------ |
| `RPUSH`  | `RPUSH` `key-name` `value` `[value...]` —— 将一个或多个值推入列表的右端 |
| `LPUSH`  | `LPUSH` `key-name` `value` `[value...]` —— 将一个或多个值推入列表的左端 |
| `RPOP`   | `RPOP` `key-name` —— 移除并返回列表最右端的元素              |
| `LPOP`   | `LPOP` `key-name` —— 移除并返回列表最左端的元素              |
| `LINDEX` | `LINDEX` `key-name` `offset` —— 返回列表中偏移量为offset的元素 |
| `LRANGE` | `LRANGE` `key-name` `start` `end` —— 返回列表从start偏移量到end偏移量范围内的所有元素，其中偏移量为start和偏移量为end的元素也会包含在被返回的元素之内 |
| `LTRIM`  |                                                              |



## 介绍

## 备注

## 疑问

