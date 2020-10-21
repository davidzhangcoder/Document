6.onsale.lua  
20201021

```
local userlist = tostring(KEYS[1]);
local productid = tostring(KEYS[2]);
local userid = tostring(ARGV[1]);
--test a
redis.debug(userlist, productid, userid);

local stock = tonumber(redis.call("get","stock:"..productid));

--has buy
if ( tonumber(redis.call('SISMEMBER',userlist,userid)) == 1 )
then
	return 0;
end

--no stock setup
if( stock == false )
then
	return 0;
end

if( stock<=0)
then
	return 0;
end

redis.call("sadd","userlist",userid);

redis.call("decr","stock:"..productid);

return 1;
```
