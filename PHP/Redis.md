#Redis

    Redis常用命令
    ------------
		select sql_name
		选择数据库sql_name
		dbsize
			返回当前数据库中key的数量
		config get *
			实时传输收到的请求
		flushdb
			删除当前选择数据库中的所有key
		flushall
			删除所有数据库中的所有key
		
		keys *
			取出所有的key
		exists
			确认一个key是否存在
		del
			删除一个key
		expire
			设置某一个key的过期时间
		move
			移动一个key的值
		get 
			获取某个key的值
		persist
			移除给定key的过期时间
		randomkey
			随机返回key空间的一个key
		rename
			重命名key
		type
			返回值的类型
		
		
		


#Redis数据类型：string,hash,list,set,zset

	string
    ------
		set name hejun
		设置key的value值，可以覆盖value值
		setnx
			setnx name hejun
			get name
			设置key对应的string类型的value值，判断value值存在否，若存在则为0，不存在则更新value值返回1

		setex
			setex haircolor 10 red
			设置key对应的value的有限时间
		setrange
			替换子字符串value值中的内容
			get name
				"junhey@qq.com"
			setrange name 7 gmail.com
				（integer）15
			get name
				junhey@gmail.com
		mset
			一次设置多个key value值
		get 
			get string类型的key值
		getrange 
			获取key的value值得子字符串
		mget
			一个获取多个key的值，如果对应的key不存在则返回nil
		incr
			对key的值做加加操作，并返回新的值
		incrby
			同incr类似，加指定的值，key不存在时候会设置key并认为原来的value是0
		decr
			对key的值做减减操作
		decrby
			同decrby类似，减指定的值
		append
			给指定的key的字符串追加value，返回新字符串值的长度。
			get name
				junhey
			append name @junhey.com
				integer 16
			get name
				junhey@junhey.com
		strlen
			取指定key的value值的长度
            
	hash类型
    --------
		hset 
			hest 表名称 表字段 表的值
			hest user:001 name junhey
		hsernx
			设置hash field为指定值，如果key不存在则先创建。如果存在返回0
		hmset
			同时设置hash的多个value值 
		hmget
			获取hash里key的所有value
		hincrby 
			获取key并加上指定值
		hexists
			测试指定field是否存在
		hlen
			返回指定field的数量
		hdel
			删除指定hash的field
		hkeys
			返回hash的所有field
		hvals
			返回hash的所有value
		hgetall
			返回hash的所有field和value
            
	列表list类型
    -------
        del mykey
            删除键mykey
        lpush mykey a b c d
            mykey键并不存在，该命令会创建该键及与其关联的List，之后在将参数中的values从左到右依次插入
        lrange mykey 0 2
            取从位置0开始到位置2结束的3个元素
        lrange mykey 0 -1
            取链表中的全部元素，其中0表示第一个元素，-1表示最后一个元素
        lpush mykey a b c d
        lpop mykey
        lpop mykey
            在执行lpop命令两次后，链表头部的两个元素已经被弹出，此时链表中元素的数量是2
            
	
	set类型
    -------
		set是集合，是string类型的无序集合，集合可以取交集，并集，差值
		sadd
			向名称为key的set中添加元素
		smembers
			查看key中的所有元素
		srem
			删除集合中key的某个元素
		spop
			随机返回并删除名称为key的set中的一个元素
		sdiff
			返回所有给定的key与第一个key的差值
		sdiffstore
			返回所有给定的key与第一个key的差值，结果存在另一个key里
		sinter
			返回给定key的交集
		sinterstore
			返回给定key的交集将结果存在另一个key值
		sunion
			返回所有给定key的并集
		sunionstore
			返回所有给定的key的并集并返回给定的key
		smove
			从一个集合里面将某个value移动另一个集合里
		scard
			返回名称为key的set的元素个数
		simember
			测试member是否是名称为key的set的元素
		srandmember
			随机返回名称为key的set的一个元素但不删除元素
		
			
	zset类型
    -------
		有序的set
		zadd
			向名称为key的zset中添加元素
		zrem
			删除名称为key的zset中的元素member
		zincrby
			以指定值key的顺序号的增加或减少
		zrank
			返回名称为key的zset中的member中的索引值
		zrevrank
			返回名称为key的zset中的member元素的排名，按score从大到小排序
		zrevrange
			返回名称为key的zset按score从大到小顺序中的index从start到end的所有元素
		zrangebyscore
			返回指定索引的key
		zcount
			返回索引的个数
		zcard
			返回所有key的个数
		zremrangebyrank
			删除集合中按指定索引区间
		zremrangebyscore
			删除按照索引号删除
			
		
		
		
		zrange myzset3 0 -1 withscores
	
