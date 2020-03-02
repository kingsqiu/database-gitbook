# 散列

## 命令

添加和删除键值对的散列操作

| 命令    | 用例和描述                                                   |
| ------- | ------------------------------------------------------------ |
| `HMGET` | `HMGET` `key-name` `key` `[key ...]`<br />从散列里面获取一个或多个的值 |
| `HMSET` | `HMSET` `key-name` `key` `value` `[key value ...]`<br />为散列里面的一个或多个键设置值 |
| `HDEL`  | `HDEL` `key-name` `key` `[key ...]`<br />删除散列里面的一个或多个键值对，返回成功找到并删除的键值对数量 |
| `HLEN`  | `HLEN` `key-name` <br />返回散列包含的键值对数量             |

散列的高级命令

| 命令           | 用例和描述                                                   |
| -------------- | ------------------------------------------------------------ |
| `HEXISTS`      | `HEXISTS` `key-name` `key` <br />检查给定键是否存在于散列中  |
| `HKEYS`        | `HKEYS` `key-name`<br />获取散列包含的所有键                 |
| `HVALS`        | `HVALS` `key-name`<br />获取散列包含的所有值                 |
| `HGETALL`      | `HGETALL` `key-name` <br />获取散列包含的所有键值对          |
| `HINCRBY`      | `HINCRBY` `key-name` `key` `increment`<br />将键`key` 存储的值加上整数`increment` |
| `HINCRBYFLOAT` | `HINCRBYFLOAT` `key-name` `key` `increment`<br />将键key存储的值加上浮点数`increment` |



## 介绍

## 备注

## 疑问