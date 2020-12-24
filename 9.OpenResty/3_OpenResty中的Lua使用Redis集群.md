3.OpenResty中的Lua使用Redis集群  
20201110  

1  
```
使用下面中的库,即rediscluster.lua 和 modem.lua
https://github.com/steve0511/resty-redis-cluster
```

2  
把rediscluster.lua 和 modem.lua 放入docker openresty容器中的 /usr/local/openresty/lualib/resty 中  

3  
在/usr/local/openresty/nginx/conf/nginx.conf加入

	lua_package_path "/usr/local/openresty/lualib/?.lua;;";
	lua_shared_dict redis_cluster_slot_locks 100k;

如：/data/?.lua 是自定义路径
```
http {
    include       mime.types;
    default_type  application/octet-stream;

	lua_package_path “/data/?.lua;/usr/local/openresty/lualib/?.lua;;";
	lua_shared_dict redis_cluster_slot_locks 100k;
```

还有，测试的路径

    location ~ /testlua/(\d+)/(\d+) {
	      lua_code_cache off;
		set $a $1;
		set $b $host;
              content_by_lua_file /data/a.lua;
    }

4  
测试代码 a.lua 如下  
```
local config = {
    dict_name = "redis_cluster_slot_locks",               --shared dictionary name for locks
    name = "testCluster",                   --rediscluster name
    serv_list = {                           --redis cluster node list(host and port),
        { ip = "192.168.1.2", port = 6379 },
        { ip = "192.168.1.2", port = 6380 },
        { ip = "192.168.1.2", port = 6381 },
        { ip = "192.168.1.2", port = 6389 },
        { ip = "192.168.1.2", port = 6390 },
        { ip = "192.168.1.2", port = 6391 }
    },
    keepalive_timeout = 60000,              --redis connection pool idle timeout
    keepalive_cons = 1000,                  --redis connection pool size
    connect_timeout = 1000,              --timeout while connecting
    max_redirection = 5,                    --maximum retry attempts for redirection
    max_connection_attempts = 1             --maximum retry attempts for connection
}

local redis_cluster = require "resty.rediscluster"
local red_c = redis_cluster:new(config)

--local v, err = red_c:hgetall("hash_test")
local v, err = red_c:hget("hash_test","hkey1")
if err then
    ngx.log(ngx.ERR, "err: ", err)
else
    ngx.say(v)
end
```
