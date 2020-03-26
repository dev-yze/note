1. sadd key member1 [member2]
2. scard key
3. sdiff key1 [key2]
4. sdiffstore destination key1 [key2]
5. sinter key1 [key2]
6. sinterstore destination key1 [key2]
7. sismember key member
8. smembers key
9. smove source destination memer
10. spop key
11. srandmember key [count]
12. srem key member1 [member2]
13. sunion key1 [key2]
14. sunionstore destination key1 [key2]
15. sscan key cursor match patterm [COUNT count]



```
> sadd set1 one two three four five six seven eight nine ten eleven
(integer) 11
> scard set1
11
> sadd set2 january fabruary march april may june july august
(integer) 8
> sadd set3 january fabruary march april may june july august september october november december
(integer) 12
> sdiff set2 set3
(empty list or set)
> sdiff set3 set2
1) "november"
2) "september"
3) "december"
4) "october"
> sinter set1 set2
(empty list or set)
> sinter set2 set3
1) "june"
2) "april"
3) "may"
4) "january"
5) "august"
6) "fabruary"
7) "march"
8) "july"
> sismember june set2
(integer) 0
> sismember set2 june
(integer) 1
> sismember set2 may
(integer) 1
> smembers set3
1) "april"
2) "june"
3) "september"
4) "january"
5) "october"
6) "august"
7) "fabruary"
8) "march"
9) "may"
10) "december"
11) "november"
12) "july"
> smembers set2
1) "june"
2) "april"
3) "may"
4) "january"
5) "august"
6) "fabruary"
7) "march"
8) "july"
> smove set3 set2 november
(integer) 1
> smembers set2
1) "june"
2) "april"
3) "may"
4) "january"
5) "august"
6) "fabruary"
7) "march"
8) "july"
9) "november"
> smembers set3
1) "april"
2) "june"
3) "september"
4) "january"
5) "october"
6) "august"
7) "fabruary"
8) "march"
9) "may"
10) "december"
11) "july"
> spop set3
"december"
> smembers set3
1) "april"
2) "june"
3) "september"
4) "january"
5) "october"
6) "august"
7) "fabruary"
8) "march"
9) "may"
10) "july"
> srem set3 october september
2
> smembers set3
1) "april"
2) "june"
3) "january"
4) "august"
5) "fabruary"
6) "march"
7) "may"
8) "july"
> sunion set1 set2
1) "eleven"
2) "two"
3) "seven"
4) "may"
5) "three"
6) "nine"
7) "eight"
8) "june"
9) "ten"
10) "six"
11) "august"
12) "march"
13) "november"
14) "four"
15) "one"
16) "april"
17) "five"
18) "january"
19) "fabruary"
20) "july"
> sunionstore set12 set1 set2
20
> smembers set12
1) "eleven"
2) "two"
3) "seven"
4) "may"
5) "three"
6) "nine"
7) "eight"
8) "june"
9) "ten"
10) "six"
11) "august"
12) "march"
13) "november"
14) "four"
15) "one"
16) "april"
17) "five"
18) "january"
19) "fabruary"
20) "july"
> sscan set1 0
1) "11"
2) 1) "seven"
2) "eleven"
3) "five"
4) "ten"
5) "four"
6) "one"
7) "three"
8) "two"
9) "eight"
10) "six"

> smembers set1
1) "four"
2) "one"
3) "five"
4) "ten"
5) "six"
6) "eleven"
7) "two"
8) "seven"
9) "three"
10) "nine"
11) "eight"
```

