String

list

set

hash

sortset



#### 一、String

1. `get key`

2. `set key keyvalue`

3. `getrange key startIndex endIndex` 返回kay的值中的子字符串

   ```
   > set sname redistest
   OK
   > get sname
   "redistest"
   > getrange sname 0 4     // 获取索引为0到4的子字符串
   "redis"
   > getrange sname 0 -1	// -1表示最后一个子字符
   "redistest"
   > getrange sname 6 -1
   "est"
   ```

   

4. `getset key value` 将指定key的值设为value,并返回key的旧值

   ```
   > set age 24
   OK
   > getset age 12
   "24"
   > getset age1 34
   (nil)
   > get age1
   "34"
   ```

   

5. `getbit key offset`

   

6. `mget key1 key2 key3` 获取多个key所对应的值

   ```
   > mget age age1
   1) "12"
   2) "34"
   ```

   

7. setbit key offset value

   

8. `setex key seconds value`  设置key的值为value,并设置key的过期时间为seonds

   ```
   > setex age3 30 105
   OK
   > get age3
   "105"
   > get age3
   "105"
   > get age3
   (nil)
   ```

   

9. `setnx key value`   如果key不存在则设置key的值

   ```
   > get age1
   "34"
   > setnx age1 30
   (integer) 0
   > setnx age2 35
   (integer) 1
   > get age2
   "35"
   ```

   

10. setrange key offset value

11. `strlen key` 返回key存储字符的长度

    ```
    > strlen age2
    (integer) 2
    > strlen sname
    (integer) 9
    ```

    

12. `mset key1 value1 key2 value2 [key value...]` 同时设置一个或多个key-value的值

13. `msetnx key1 value1 key2 value2 [key value...]` 同时设置一个或多个key-value的值，当且仅当所有给定的key都不存在

    ```
    > mset user1 username1 user2 username2 user3 username3
    OK
    > get user1
    "username1"
    > get user2
    "username2"
    > get user3
    "username3"
    > msetnx user1 username1 mobile2 mobilename2 mobile3 mobilename3
    (integer) 0
    > get user1
    "username1"
    > get mobile2
    (nil)
    > msetnx mobile1 mobilename1 mobile2 mobilename2 mobile3 mobilename3
    (integer) 1
    > get mobile2
    "mobilename2"
    ```

14. `incr key`

15. incrby key increment

16. incrbyfloat key increment

    ```
    > get age1
    "34"
    > incr age
    (integer) 13
    > incr age1
    (integer) 35
    > get age1
    "35"
    > incrby age1 10
    (integer) 45
    > set weight 48.4
    OK
    > incrbyfloat weight 0.6
    49.0
    ```

17. `decr key`

18. `decrby key decrement`

19. `append key value`  如果key已经存在且是一个字符串，将value追加到其末尾

    ```
    > get sname
    "redistest"
    > append sname helloworld
    19
    > get sname
    "redistesthelloworld"
    ```

    

 