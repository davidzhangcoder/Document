5_1.lua集群注意事项
20201026

1.
集群环境的Lua, 所用key必须通过KEYS[]传入，否则会报以下错误  
Lua script attempted to access a non local key in a cluster node

2.集群环境运行Lua的错误  
(1)  
(重要)  
运行Lua脚本，如以下的testlua.lua, 它所对应的SHA值所对应的SLOT值，必须在6390所对应的实例上  
否则会报： (error) CROSSSLOT Keys in request don't hash to the same slot  
```
redis-cli -c -p 6390 --eval testlua.lua userlist , 1
```

在Redis集群版实例中，事务、脚本等命令要求的key必须在同一个slot中，如果不在同一个slot将返回错误信息：command keys must in same slot.  
见- https://www.cnblogs.com/June2005/p/11457006.html

(2)  
集群环境中，Lua脚本中所用的Key必须在同一个实例上，可以用{} - 即Hash Tag来解决

3.集群环境运行Lua的步骤  
共四步－第一步：通过以下命令得到SHA值
redis-cli -c -p 6381 script load "$(cat testlua.lua)"

共四步－第二步：通过以下命令得到SHA值对印的SLOT
cluster keyslot 4c7df8182515cecd2dcfdc8f8f3aa42dd707142c

共四步－第三步：通过以下命令得到SLOT对印的实例
cluster nodes

共四步－第四步：前往对印的实例，并复制相应的Lua文件，通过以下命令执行Lua
redis-cli -c -p 6390 --eval testlua.lua userlist , 1
