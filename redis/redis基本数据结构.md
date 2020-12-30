* redis基本数据结构
	- string:字符串
		- 基础语法
			- 设置 set key value [EX seconds|PX milliseconds|KEEPTTL] [NX|XX]
				- key 键
				- value 值
				- Ex seconds 过期秒数
				- PX 过期毫秒数
				- NX 只在键不存在时,才对键进行设置操作(锁)
				- XX 只有键存在时,才能对键进行设置操作
				- 例子:		
					1. 在键test不存在的情况下,设置值为l,并且过期时间为10秒<br>
					set test l EX 10 NX 
					2. 在键test存在的情况下,设置值为x并且过期时间为10毫秒<br>
					set test x PX 10 XX
			- 获取 get key
				- 例子:
					1. 获取键test<br>
					get test
	- Hash:散列
		- 基础语法
			- 设置 hset key field value [field value ...]
				- key 键
				- field 字段
				- value 值
				- 例子:
					1. 设置键test,字段为name,值l<br>
					hset test name l
					2. 设置键test,字段name,值l,字段age,值10<br>
					hset test name l age 10
			- 获取
				1. hgetall key 获取该key的全部数据 (hgetall test)
				2. hget key field 获取该key的field字段的值 (hget test name)
				3. hmget key field [field] 获取改key多个字段的值 (hmget test name age)
	- List:列表（有序,简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）或者尾部（右边））
		- 基础语法
			- 设置 LPUSH key element [element ...]
				- key 键
				- element 值
				- 例子 
					1. 设置键为test 值为0,1,2,3<br>
					lpush  test 0 1 2 3
			- 获取 Lrange key start stop
				- key 键
				- start 起始位置 (从0开始)
				- stop  结束位置 (-1为结尾)
				- 例子
					1. 获取键为test 前三个值<br>
					lrange test 0 2
					2. 获取键为test 所有值<br>
					lrange test 0 -1
	- Set:集合（无序,集合成员是唯一的，这就意味着集合中不能出现重复的数据）
		- 基础语法
			- 设置 sadd key member [member ...]
				- key 键
				- member 值
				- 例子 
					1. 设置键为stest 值为0,1,2,3<br>
					sadd stest 0 1 2 3
			- 获取 smembser key
				- key 键
				- 例子
				  1. 获取键为stest<br>
					smembers stest
	- Sorted Set:有序集合(每个元素都会关联一个 double 类型的分数。redis 正是通过分数来为集合中的成员进行从小到大的排序)
		- 基础语法
			- 设置 zadd key [NX|XX] [CH] [INCR] score member [score member ...]
				- key 键
				- NX 只在键不存在时,才对键进行设置操作
				- XX 只有键存在时,才能对键进行设置操作 
				- CH 返回有更新的个数（默认返回添加的个数）
				- 例子 
					1. 设置键为ztest 分数0,值test1,分数1,值test2<br>
					zadd ztest 0 test1 1 test2
					2. 设置键为ztest 只有键存在才进行设置,分数0,值test1,分数2,值test3 返回更新个数<br>
					zadd ztest nx ch 0 test1 2 test3
			- 获取 ZRANGE key start stop [WITHSCORES]
				- key 键
				- start 起始位置 (从0开始)
				- stop  结束位置 (-1为结尾)
				- WITHSCORES 显示分数
				- 例子
				  1. 获取键为ztest的数据,并且显示分数<br>
				  zrange ztest 0 -1 withscorces
				  2. 获取键为ztest的数据第一个数据,并且不显示分数<br>
				  zrange ztest 0 0
								
		
	
