9.Redis Docker命令 和 配置文件  
20201024

1  
在/Users/davidzhang/Documents/dockerworkspace/redis/建立redis-6379.conf  
容器中应该有/data路径  
-v是使用docker volume  

以下命令是用redis-6379.conf配置文件启动redis，其他端口做相应修改
```
docker run -v /Users/.../Documents/dockerworkspace/redis/redis-6379.conf:/data/redis-6379.conf --name redis-6379 -d redis redis-server /data/redis-6379.conf
```

**redis-6379.conf内容如下(RDB配置文件),**   
daemonize必须配成no或注释掉，不然不能启动   
并且用RDB方式持久化

	port 6379
	daemonize no
	logfile “6379.log” (注意替换引号为英文字符)
	dir /data
	dbfilename dump.rdb
	rdbcompression yes
	save 900 1
	save 30 5
	save 60 10000

2  
举例建立6380  
```
docker run -v /Users/davidzhang/Documents/dockerworkspace/redis/redis-6380.conf:/data/redis-6380.conf --name redis-6380 -d redis redis-server /data/redis-6380.conf
```
redis-6380.conf内容如下(RDB配置文件)   

	port 6380
	daemonize no
	logfile “6380.log” (注意替换引号为英文字符)
	dir /data
	dbfilename dump.rdb
	rdbcompression yes
	save 900 1
	save 30 5
	save 60 10000

3  
举例AOF配置文件：  
**注意 - RDB和AOF同时开启，系统默认取AOF的数据 (同时开启 - 即去掉＃注释)**  

	port 6380
	daemonize no
	logfile “6380.log” (注意替换引号为英文字符)
	dir /data
	＃dbfilename dump.rdb
	＃rdbcompression yes
	＃save 900 1
	＃save 30 5
	＃save 60 10000
	appendonly yes
	appendfilename “appendonly.aof” (默认为appendonly.aof, 注意替换引号为英文字符)
	appendfsync everysec
	auto-aof-rewrite-percentage 100 (默认)
	auto-aof-rewrite-min-size 64mb (默认)

4  
查看配置信息  
CONFIG 命令查看或设置配置项。   
CONFIG get * 所有的  
 CONFIG get XXX  
 CONFIG set XXX YYY (设置XXX = YYY)   