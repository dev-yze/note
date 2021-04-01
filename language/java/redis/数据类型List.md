1. blpop key1 [key2] timeout

2. brpop key1 [key2] timeout

3. brpoplpush source destination timeout

4. `lindex key index`

5. `linsert key before|after pivot value`

6. `llen key`

7. `lpop key`   移除列表中的第一个元素

8. `lpush key value1 [vlaue2]`

9. `lpushx key value`

10. `lrange key start end`

11. `lrem key count value`  移除key列表中的value值

    count > 0 : 从表头开始向表尾搜索，移除与value相等的元素，数量为count

    count < 0 : 从表尾开始向表头搜索，移除与value相等的元素，数量为count的绝对值

    count = 0 : 移除表中所有与value相等的值

12. `lset key index value`

13. `ltrim key start stop`

14. `rpop key`     移除列表中的最后一个元素

15. rpoplpush source destination

16. rpush key value1 [value2]

17. rpushx key value

    ```
    > lpush list8 name1 name2 name3 name4  // 创建列表8，push元素
    (integer) 4
    > lrange list8 0 -1			// 查询某范围内的元素
    1) "name4"
    2) "name3"
    3) "name2"
    4) "name1"
    > lindex list8 0			// 按索引查询元素
    "name4"
    > lindex list8 1
    "name3"
    > lindex list8 2
    "name2"
    > lindex list8 3
    "name1"
    > lindex list8 4
    (nil)
    > llen list8				// 查询列表长度
    (integer) 4
    > lpop list8				// 移除并获取第一个元素
    "name4"
    > llen list8
    (integer) 3
    > lrange list8 0 -1
    1) "name3"
    2) "name2"
    3) "name1"
    > lpush list8 name5
    (integer) 4
    > lrange list8 0 -1
    1) "name5"
    2) "name3"
    3) "name2"
    4) "name1"
    > lpushx list7 name7			// 向存在的list中插入元素
    (integer) 0
    > lpushx list8 name6			
    (integer) 5
    > lrange list8 0 -1
    1) "name6"
    2) "name5"
    3) "name3"
    4) "name2"
    5) "name1"
    > lindex list8 0
    "name6"
    > linsert list8 before name3 name4
    6
    > lrange list8 0 -1
    1) "name6"
    2) "name5"
    3) "name4"
    4) "name3"
    5) "name2"
    6) "name1"
    > linsert list8 after name3 name21		// 往列表中某一存在的元素之前或之后插入元素
    7
    > lrange list8 0 -1
    1) "name6"
    2) "name5"
    3) "name4"
    4) "name3"
    5) "name21"
    6) "name2"
    7) "name1"
    > lpush list8 name4
    (integer) 8
    > lrange list8 0 -1
    1) "name4"
    2) "name6"
    3) "name5"
    4) "name4"
    5) "name3"
    6) "name21"
    7) "name2"
    8) "name1"
    > lrem list8 1 name4
    (integer) 1
    > lrange list8 0 -1
    1) "name6"
    2) "name5"
    3) "name4"
    4) "name3"
    5) "name21"
    6) "name2"
    7) "name1"
    > lpush list8 name3
    (integer) 8
    > lrange list8 0 -1
    1) "name3"
    2) "name6"
    3) "name5"
    4) "name4"
    5) "name3"
    6) "name21"
    7) "name2"
    8) "name1"
    > lrem list8 0 name3				// 删除元素
    (integer) 2
    > lrange list8 0 -1
    1) "name6"
    2) "name5"
    3) "name4"
    4) "name21"
    5) "name2"
    6) "name1"
    > lset list8 0 name61		// 按索引设置值
    OK
    > lrange list8 0 -1			
    1) "name61"
    2) "name5"
    3) "name4"
    4) "name21"
    5) "name2"
    6) "name1"
    > ltrim list8 2 4
    OK
    > lrange list8 0 -1				// 按索引裁剪list,范围之外删除
    1) "name4"
    2) "name21"
    3) "name2"
    > rpop list8					// 移除列表最后一个元素并返回
    "name2"
    > rpush list8 value1 value2 value3		// 向列表末尾添加元素
    (integer) 5
    > lrange list8 0 -1
    1) "name4"
    2) "name21"
    3) "value1"
    4) "value2"
    5) "value3"
    > rpushx list8 value4  						// 向存在的列表末尾插入一个元素
    (integer) 6
    > lrange list8 0 -1							
    1) "name4"
    2) "name21"
    3) "value1"
    4) "value2"
    5) "value3"
    6) "value4"
    > rpoplpush list8 list9    					// 移除list8中最后一个元素插入list9的开头
    "value4"
    > lrange list8 0 -1
    1) "name4"
    2) "name21"
    3) "value1"
    4) "value2"
    5) "value3"
    > lrange list9 0 -1
    1) "value4"
    ```
    
    