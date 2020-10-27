11.Redis集群的配置 和 集群相关命令  
20201025

1.共三步：第一步  
建立配置文件  
redis-cluster-6379.conf内容如下(其他文件要把6379改成相应数字):

```
port 6379
daemonize no
logfile "6379.log"
dir /data

save 900 1
save 30 5
save 60 10000

	appendonly no
	appendfilename "appendonly.aof"
	appendfsync everysec
	auto-aof-rewrite-percentage 100 
	auto-aof-rewrite-min-size 64mb 

cluster-enabled yes
cluster-config-file nodes-6379.conf
cluster-node-timeout 15000
```

2.共三步：第二步  
开启6个Redis实例，集群必须要有3个主服务器(以下配置是每个主服务器有一个从服务器)  
```
docker run -v /Users/davidzhang/Documents/dockerworkspace/redis/redis-cluster-6379.conf:/data/redis-cluster-6379.conf --name redis-cluster-6379 -p 6379:6379 -d redis redis-server /data/redis-cluster-6379.conf

docker run -v /Users/davidzhang/Documents/dockerworkspace/redis/redis-cluster-6380.conf:/data/redis-cluster-6380.conf --name redis-cluster-6380 -p 6380:6380 -d redis redis-server /data/redis-cluster-6380.conf

docker run -v /Users/davidzhang/Documents/dockerworkspace/redis/redis-cluster-6381.conf:/data/redis-cluster-6381.conf --name redis-cluster-6381 -p 6381:6381 -d redis redis-server /data/redis-cluster-6381.conf


docker run -v /Users/davidzhang/Documents/dockerworkspace/redis/redis-cluster-6389.conf:/data/redis-cluster-6389.conf --name redis-cluster-6389 -p 6389:6389 -d redis redis-server /data/redis-cluster-6389.conf

docker run -v /Users/davidzhang/Documents/dockerworkspace/redis/redis-cluster-6390.conf:/data/redis-cluster-6390.conf --name redis-cluster-6390 -p 6390:6390 -d redis redis-server /data/redis-cluster-6390.conf

docker run -v /Users/davidzhang/Documents/dockerworkspace/redis/redis-cluster-6391.conf:/data/redis-cluster-6391.conf --name redis-cluster-6391 -p 6391:6391 -d redis redis-server /data/redis-cluster-6391.conf
```

3.共三步：第三步  
使用docker inspect来获得docker的地址  
```
docker inspect  redis-cluster-6379 | grep IPAddress **(必须要获得docker的地址来组合集群，如：172.17.0.2)**
```
进入redis-cluser-6379的docker容器(docker exec -it redis-cluster-6379 /bin/bash), 执行以下命令，组合成集群， --cluster-replicas 1 表示为集群中的每个主节点创建一个从节点  
```
redis-cli --cluster create 172.17.0.2:6379, 172.17.0.3:6380, 172.17.0.4:6381, 172.17.0.5:6389, 172.17.0.6:6390, 172.17.0.7:6391 --cluster-replicas 1
```

4.共四步：第四步  
把相应地址，如：172.17.0.2， 映射到本机  
```
sudo ifconfig lo0 alias 172.17.0.2
sudo ifconfig lo0 alias 172.17.0.3
sudo ifconfig lo0 alias 172.17.0.4
sudo ifconfig lo0 alias 172.17.0.5
sudo ifconfig lo0 alias 172.17.0.6
sudo ifconfig lo0 alias 172.17.0.7
```

用完后，可以用以下命令移除  
```
sudo ifconfig lo0 -alias 172.17.0.2
sudo ifconfig lo0 -alias 172.17.0.3
sudo ifconfig lo0 -alias 172.17.0.4
sudo ifconfig lo0 -alias 172.17.0.5
sudo ifconfig lo0 -alias 172.17.0.6
sudo ifconfig lo0 -alias 172.17.0.7
```

5.集群相关命令
```
cluster nodes - 查看集群相关信息

cluster keyslot <key> - 计算键key应该被放置在哪个slot上

cluster countkeysinslot <slot> - 返回槽slot目前包含的键值对数量

cluster getkeysinslot <slot> <count> - 返回 count 个slot槽中的键

CLIENT LIST            - 获取客户端列表

CLIENT SETNAME   - 设置当前连接点redis的名称

CLIENT GETNAME   - 查看当前连接的名称

CLIENT KILL ip:port   - 杀死指定连接

info clients - 可以查看当前的redis连接数

config get maxclients - 可以查询redis允许的最大连接数

```


6.集群相关的概念

* 不在一个slot下的键值，是不能使用mget,mset等多键操作

* 可以通过{}来定义组的概念，从而使key1中{}内相同内容的键值对放到同一个slot中去

* redis.conf中的参数 cluster-require-full-coverage 是指16384个slot都正常的时候集群才能对外提供服务


7.手动命令行建集群

* Mac 搭建 Redis 集群 － https://www.jianshu.com/p/a32542ce4c0b

