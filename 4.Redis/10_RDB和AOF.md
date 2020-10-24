10.RDB和AOF  
20201024

1  
RDB保存数据  

> 优点:
> * 节省空间  
> * 恢复速度快  

> 缺点：  
> * 如数据庞大，消耗性能  
> * 会丢失最后一次快照后所有的修改  

> **触发持久化的条件**  
> * 满足save的条件  
> * 正常shutdown关闭
		

2
AOF保存每个写操作的指令

	(1)
	AOF默认不开启，需要手动在配置文件中开启

	appendonly yes
	appendfilename “appendonly.aof” (默认为appendonly.aof)

	AOF文件的保存路径，同RDB的路径一致

	(2)
	AOF同步频率
		始终同步 － 每次同步
		每秒同步
		不主动同步，把同步时机交给操作系统

		配置举例：
		appendfsync always 始终同步 － 每次同步
		appendfsync everysec 每秒同步
		appendfsync no 不主动同步，把同步时机交给操作系统

	(3)
	AOF Rewrite - 重写
	当到达一定值后，用最小指令集重写AOF文件(将整个内存中的数据用命令的方式重写一个新的AOF文件, 这点和快照有点类似)

	系统载入时或者上次重写完毕时， Redis会记录此时AOF大小，设为base_size,如果Redis 的AOF当前大小>=base_size+base_size*100%(默认)且当前大小>=64mb(默认)的情况下，Redis会对AOF进行重写

	auto-aof-rewrite-percentage 100
	auto-aof-rewrite-min-size 64mb

	(4)
	缺点：
		比起RDB占用更多的磁盘空间
		恢复备份速度要慢

3  
**RDB和AOF同时开启，系统默认取AOF的数据**

**官方推荐RDB和AOF两个一起用**