

1. `hdel key field1 [field2]`
2. `hexists key field`
3. `hget key field`
4. `hgetall key`
5. `hincrby key field increment`
6. `hincrbyfloat key field increment`
7. `hkeys key`
8. `hlen key`
9. `hmget key field1 [field2]`
10. `hmset key field1 value1 [field2 value2]`
11. `hset key field value`
12. `hsetnx key field value`
13. `hvalues key`
14. `hscan key cursor [MATCH pattern] [COUNT count]`





```
> hset hash1 name yang  // 设置hash map
(integer) 1
> hget hash1 name		// 获取map中属性值
"yang"
> hmset hash1 age 23 sex 男 address anhui  // 批量设置map中属性值
OK
> hmget hash1 name age sex  //批量获取map中属性值
1) "yang"
2) "23"
3) "男"
> hgetall hash1			// 获取map中所有值
1) "name"
2) "yang"
3) "age"
4) "23"
5) "sex"
6) "男"
7) "address"
8) "anhui"
> hdel hash1 sex    // 删除map中字段
(integer) 1
> hgetall hash1
1) "name"
2) "yang"
3) "age"
4) "23"
5) "address"
6) "anhui"
> hlen hash1	// map长度
3
> hkeys hash1	// map中所有key
1) "name"
2) "age"
3) "address"
> hvals hash1	// map中所有value
1) "yang"
2) "23"
3) "anhui"
> hincrby hash1 age 12   // 字段增加值
(integer) 35
> hgetall hash1
1) "name"
2) "yang"
3) "age"
4) "35"
5) "address"
6) "anhui"
> hsetnx hash1 weight 78.3	// 属性不存在则增加
(integer) 1
> hgetall hash1
1) "name"
2) "yang"
3) "age"
4) "35"
5) "address"
6) "anhui"
7) "weight"
8) "78.3"
> hincrbyfloat hash1 weight 0.2		// 属性增加浮点值
78.5
> hgetall hash1
1) "name"
2) "yang"
3) "age"
4) "35"
5) "address"
6) "anhui"
7) "weight"
8) "78.5"
```

