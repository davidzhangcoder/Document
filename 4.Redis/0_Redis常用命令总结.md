0.Redis常用命令总结  
20201029

1.控制台  
```
redis-server redis-6379.conf - 从配置文件启动

redis-cli -h <ip> -p <port> - -h默认是127.0.0.1
redis-cli -p 6380

cat reds.conf | grep -v “#” | grep -v “^$” - 简化配置文件
cat reds.conf | grep -v “#” | grep -v “^$” > redis-6379.conf
```

2.LUA   
```
(1)运行
redis-cli --eval test.lua key1 key1

(2)调试
redis-cli --ldb --eval test.lua key1 key1

(3)装入redis,并返回sha1 tag
redis-cli script load "$(cat test.lua)"

(4)同步模式
redis-cli --ldb-sync-mode --eval /tmp/script.lua
```

3.主从复制   
```
info replication - 打印主从复制的相关信息

slaveof <主服务器ip> <主服务器port> - 成为某个实例的从服务器

slaveof no one - 不做任何一台服务器的从服务器
```

4.服务器端  
```
(1)
查看配置信息
CONFIG 命令查看或设置配置项。 CONFIG get * 所有的 CONFIG get XXX CONFIG set XXX YYY (设置XXX = YYY)

(2)
集群相关命令
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
