# 字符串

## 命令

基本命令

| 命令  | 行为                                   |
| ----- | -------------------------------------- |
| `GET` | 获取存储在给定键中的值                 |
| `SET` | 设置存储在给定键中的值                 |
| `DEL` | 删除存储在给定键中的值（所有类型可用） |

自增自减命令（[备注]())

| 命令          | 用例与描述                                                   |
| ------------- | ------------------------------------------------------------ |
| `INCR`        | `INCR` `key-name` <br />将键存储的值加1                      |
| `DECR`        | `DECR` `key-name`<br /> 将键存储的值减1                      |
| `INCRBY`      | `INCRBY` `key-name` `amount` <br />将键存储的值加上整数`amount` |
| `DECRBY`      | `DECRBY` `key-name` `amount`<br />将键存储的值减去整数`amount` |
| `INCRBYFLOAT` | `INCRBYFLOAT` `key-name` `amount`<br />将键存储的值加上浮点数`amount`。Redis2.6以上可用 。 |

供Redis处理子串和二进制位的命令（[备注]())

| 命令       | 用例与描述                                                   |
| ---------- | ------------------------------------------------------------ |
| `APPEND`   | `APPEND` `key-name` `value` <br /> 将值value追加到给定键key-name当前存储的值的末尾 |
| `GETRANGE` | `GETRANGE` `key-name`  `start` `end` <br /> 获取一个由偏移量start至偏移量end范围内所有字符组成的子串，包括start和end在内 |
| `SETRANGE` | `SETRANGE` `key-name` `offset` `value` <br />将从start偏移量开始的子串设置为给定值 |
| `GETBIT`   | `GETBIT` `key-name` `offset` `value` <br />将字节串看作是二进制位串（bit string），并返回位串中偏移量为offset的二进制位的值 |
| `SETBIT`   | `SETBIT` `key-name` `offset` `value` <br />将字节串看作是二进制位串，并将位串中偏移量为offset的二进制位的值设置为value |
| `BITCOUNT` | `BITCOUNT` `key-name` `[start end]` <br /> 统计二进制位串里面为1的二进制位的数量，如果给定了可选的start偏移量和end偏移量，那么只对偏移量指定范围内的二进制位进行统计 |
| `BITOP`    | `BITOP` `operation` `dest-key`  `key-name` `[keyname...]` <br />对一个或多个二进制位串执行包括并(AND)、或(OR)、异或(XOR)、非(NOT)在内的任意一种按位运算操作(bitwise operation)，并将计算得出的结果保存在dest-key键里面 |



## 介绍

字符串可以存储三种类型的值

- 字符串
- 整数
- 浮点数

## 备注

## 疑问

