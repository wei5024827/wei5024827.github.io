#### 1.连续登录问题

总结

- 首先按照日期进行排序，然后计算出rank值
- 用时间减去rank值，得到的新时间都相等的则是连续的
- 然后按照新的时间分组，进行count计算，就是连续的天数

找出连续登录三天的用户，且用户每天的lowcarbon>100

```
id 		dt 			lowcarbon
1001 	2021-12-12 	123
1002	2021-12-12 	45
1001 	2021-12-13 	43
1001 	2021-12-13 	45
1001 	2021-12-13 	23
1002 	2021-12-14 	45
1001 	2021-12-14 	230
1002 	2021-12-15 	45
1001 	2021-12-15 	23
… …
```

```sql
--每天lowcarbon>100的用户
select 
	id,
	dt,
	sum(lowcarbon) lowCount
from tb1
group by id,dt
having lowCount > 100;t1

--等差数列，两个等差数列，如果等差相同，则相同位置的数据相减得到的结果相同
--按照用户分组，同时按照时间排序，计算每天数据的rank值
select
id,
dt,
lowCount,
rank() over(partition by id order by dt) rk
from t1;t2

--日期减去rank值
select 
id,
dt,
lowCount
date_sub(dt,rk) datediff
from t2;t3

id 		dt 			lowcarbon	rk datediff
1001 	2021-12-12 	123			1	2021-12-11
1001 	2021-12-13 	101			2	2021-12-11
1001 	2021-12-14 	230			3	2021-12-11


--按照用户及datediff分组，求每个组有多少条数据，并找出大于等于3的
select 
id,
datediff,
count(*) ct
from 
(
    select 
		id,
		dt,
		lowCount
		date_sub(dt,rk) datediff
	from 
    (
        select
			id,
			dt,
			lowCount,
			rank() over(partition by id order by dt) rk
		from 
        (
			select 
				id,
				dt,
				sum(lowcarbon) lowCount
			from tb1
			group by id,dt
			having lowCount > 100
        )
    )
)
group by id,datediff
having ct>=3;
```



#### 2.间隔时间分组问题

总结：

- 将时间偏移到下一组，然后两个时间相减得到差值
- 计算从第一行到当前行差值大于等于60的总个数，即为组号

```
如下为电商公司用户访问时间数据
id 		ts(秒)
1001 17523641234
1001 17523641256
1002 17523641278
1001 17523641334
1002 17523641434
1001 17523641534
1001 17523641544
1002 17523641634
1001 17523641638
1001 17523641654

```

某个用户连续的访问记录如果时间间隔小于 60 秒，则分为同一个组，结果为：

```
id   ts(秒) 		group
1001 17523641234 1
1001 17523641256 1
1001 17523641334 2
1001 17523641534 3
1001 17523641544 3
1001 17523641638 4
1001 17523641654 4
1002 17523641278 1
1002 17523641434 2
1002 17523641634 3
```

```sql
--将上一行ts数据下移
select 
	id,
	ts,
	lag(ts,1,0) over(partition by id order by ts) lagts
from table2;t1

--将当前行时间数据减去上一行时间数据
select 
	id,
	ts,
	ts-lagts tsdiff
from 
	t1;t2
	
--计算每个用户范围内从第一行到当前行tsdiff大于等于60的总个数，相当于分组的组号
select 
	id,
	ts,
	sum(if(tsdiff>=60,1,0)) over(partition by id order by ts) groupid
from 
	(select 
		id,
		ts,
		ts-lagts tsdiff
	from 
		(
    	select 
			id,
			ts,
			lag(ts,1,0) over(partition by id order by ts) lagts
		from 
        	table2)
     );
```

#### 3.间隔连续问题

总结

- 把上一条数据下移，计算差值
- 计算从第一个到这一行大于2的个数flag
- 按照flag分组，计算这一组最大日期减最小日期的差值+1
- 所有数据都计算出来后，max为最后的最大连续登录天数

```
id   dt
1001 2021-12-12
1002 2021-12-12
1001 2021-12-13
1001 2021-12-14
1001 2021-12-16
1002 2021-12-16
1001 2021-12-19
1002 2021-12-17
1001 2021-12-20

```

计算每个用户最大的连续登录天数，可以间隔一天。ps：如果是1，3，5，6，则视为连续6天登录

```sql
--思路一：等差数列
--思路二：分组
--将上一行时间数据下移,并计算差值datediff(dt1,dt2)
1001 2021-12-12  1970-01-01  569988
1001 2021-12-13  2021-12-12  1
1001 2021-12-14	 2021-12-13  1
1001 2021-12-16	 2021-12-14  2
1001 2021-12-19  2021-12-16  3
1001 2021-12-20  2021-12-19  1
select 
	id,
	dt,
	dt2,
	datediff(dt,dt2) flag
from
(
	select 
		id,
		dt,
		lag(dt,1) over(partition by id order by dt) dt2
	from table3
    ) ;t1

--按照用户分组，同时按照时间排序，计算从第一行到当前行大于2的数据的总条数(sum(if(flag>2,1,0)))
1001 2021-12-12  1970-01-01  569988 1
1001 2021-12-13  2021-12-12  1		1
1001 2021-12-14	 2021-12-13  1		1
1001 2021-12-16	 2021-12-14  2		1
1001 2021-12-19  2021-12-16  3		2
1001 2021-12-20  2021-12-19  1		2
select 
	id,
	dt,
	flag,
	sum(if(flag>2,1,0)) over(partition by id order by dt) flag2
from t1;t2
	
--按照用户和flag分组，求最大时间减去最小时间并加上1
1001 2021-12-12  1970-01-01  569988 1 
1001 2021-12-13  2021-12-12  1		1
1001 2021-12-14	 2021-12-13  1		1
1001 2021-12-16	 2021-12-14  2		1
1001 2021-12-19  2021-12-16  3		2
1001 2021-12-20  2021-12-19  1		2
select 
	id,
	flag2,
	max(dt)-min(dt)+1 days
from t2
group by flag2;
t3
	
--取连续登录天数的最大值
select 
	id,
	max(days)
from t3
group by id
```

```sql
--最终sql
select 
	id,
	max(days)
from 
(
    select 
		id,
		flag2,
		max(dt)-min(dt)+1 days
	from (
    	select 
			id,
			dt,
			flag,
			sum(if(flag>2,1,0)) over(partition by id order by dt) flag2
		from 
        (
            select 
				id,
				dt,
				dt2,
				datediff(dt,dt2) flag
			from
			(
				select 
					id,
					dt,
					lag(dt,1) over(partition by id order by dt) dt2
				from table3
    		) 
        )
    )
	group by flag2
)
group by id
```



#### 4.打折日期交叉问题

```
brand stt edt
oppo 2021-06-05 2021-06-09
oppo 2021-06-11 2021-06-21
vivo 2021-06-05 2021-06-15
vivo 2021-06-09 2021-06-21
redmi 2021-06-05 2021-06-21
redmi 2021-06-09 2021-06-15
redmi 2021-06-17 2021-06-26
huawei 2021-06-05 2021-06-26
huawei 2021-06-09 2021-06-15
huawei 2021-06-17 2021-06-21
```

计算每个品牌总的打折销售天数，注意其中的交叉日期，比如 vivo 品牌，第一次活动时 间为 2021-06-05 到 2021-06-15，第二次活动时间为 2021-06-09 到 2021-06-21 其中 9 号到 15 号为重复天数，只统计一次，即 vivo 总打折天数为 2021-06-05 到 2021-06-21 共计 17 天。

#### 5.同时在线人数

总结：

- 开始时间标记为1，结束时间标记为-1，进行union
- 按照时间排序，将标记相加
- 然后用sum函数求出最多人数

```
+------------+-------------+-------------+
| table6.id  | table6.stt  | table6.edt  |
+------------+-------------+-------------+
| 1001       | 12:12:12    | 18:12:12    |
| 1003       | 13:12:12    | 16:12:12    |
| 1004       | 13:15:12    | 20:12:12    |
| 1002       | 15:12:12    | 16:12:12    |
| 1005       | 15:18:12    | 20:12:12    |
| 1001       | 20:12:12    | 23:12:12    |
| 1006       | 21:12:12    | 23:15:12    |
| 1007       | 22:12:12    | 23:10:12    |
+------------+-------------+-------------+

```

根据该数据计算出平台最高峰同时在线的主播

```sql
----首先开播记为1，下播记为-1
select id,stt dt,'1' p from table6
union
select id,edt dt,'-1' p from table6

+---------+-----------+--------+
| _u1.id  |  _u1.dt   | _u1.p  |
+---------+-----------+--------+
| 1001    | 12:12:12  | 1      |
| 1001    | 18:12:12  | -1     |
| 1001    | 20:12:12  | 1      |
| 1001    | 23:12:12  | -1     |
| 1002    | 15:12:12  | 1      |
| 1002    | 16:12:12  | -1     |
| 1003    | 13:12:12  | 1      |
| 1003    | 16:12:12  | -1     |
| 1004    | 13:15:12  | 1      |
| 1004    | 20:12:12  | -1     |
| 1005    | 15:18:12  | 1      |
| 1005    | 20:12:12  | -1     |
| 1006    | 21:12:12  | 1      |
| 1006    | 23:15:12  | -1     |
| 1007    | 22:12:12  | 1      |
| 1007    | 23:10:12  | -1     |
+---------+-----------+--------+


----按照时间排序，对上线下线结果累加
select id,dt,
sum(p) over(order by dt) sum_p
from
(select id,stt dt,'1' p from table6
union
select id,edt dt,'-1' p from table6)t1;
+-------+-----------+--------+
|  id   |    dt     | sum_p  |
+-------+-----------+--------+
| 1001  | 12:12:12  | 1.0    |
| 1003  | 13:12:12  | 2.0    |
| 1004  | 13:15:12  | 3.0    |
| 1002  | 15:12:12  | 4.0    |
| 1005  | 15:18:12  | 5.0    |
| 1003  | 16:12:12  | 3.0    |
| 1002  | 16:12:12  | 3.0    |
| 1001  | 18:12:12  | 2.0    |
| 1005  | 20:12:12  | 1.0    |
| 1001  | 20:12:12  | 1.0    |
| 1004  | 20:12:12  | 1.0    |
| 1006  | 21:12:12  | 2.0    |
| 1007  | 22:12:12  | 3.0    |
| 1007  | 23:10:12  | 2.0    |
| 1001  | 23:12:12  | 1.0    |
| 1006  | 23:15:12  | 0.0    |
+-------+-----------+--------+

----求出在线人数的最大值
select 
max(sum_p)
from(
select id,dt,
sum(p) over(order by dt) sum_p
from
(select id,stt dt,'1' p from table6
union
select id,edt dt,'-1' p from table6));
+------+
| _c0  |
+------+
| 5.0  |
+------+
```



#### 6.每日增量sql

```sql
--sale_order 昨日订单表
--sale_order_inc 今日订单全量表

select *,
row_number() over(partition by order_id order by last_update_time desc) as rn
from (select * from sale_order union  sale_order_inc ) a
where rn = 1
```



#### 7.三种rank

![image-20220609094249005](C:\Users\wei50\AppData\Roaming\Typora\typora-user-images\image-20220609094249005.png)



#### 8.窗口函数

over(partition by xxx order by xxx) 按照哪个字段分组，按照哪个字段排序

range between指定当前行的取值范围

rows between指定order by后前N行及后N行的数据计算

- UNBOUNDED PRECEDING ：对上限无限制
- UNBOUNDED FOLLOWING ：对下限无限制
- PRECEDING ： 当前行之前的 n 行 （ n 表示具体数字如：5 PRECEDING ）
- FOLLOWING ：当前行之后的 n 行 （ n 表示具体数字如：5 FOLLOWING ）
- CURRENT ROW ：仅当前行









