2.常用指令和module, 和一些细节  
20201109

1  
lua_code_cache

2  
error_log的默认值：
```
#error_log  logs/error.log  error;
```

3  
当 lua_code_cache on 开启时，require 加载的模块是会被缓存下来的，这样我们的模块就会以最高效的方式运行，直到被显式地调用如下语句（这里有点像模块卸载）：
```
package.loaded["square"] = nil
```

4  
```
obj = { x = 20 };
obj1 = { x = 30 }
function obj.fun1(self)
    ngx.say(self.x)
end
obj.fun1(obj1); -- 其实self不用传入本身对象，只是指：如果要使用本身对象，必须手动传入
```

5  
--ngx.say(testModule1.method3()) --如在testModule这么定义：function method3()，会报错：attempt to call field 'method3' (a nil value)，因为 method3()是作为全局变量  

--ngx.say(method3()) --如在testModule这么定义：function method3()，正常运行，因为是调用全局变量，但会有警告：writing a global Lua variable ('method3') which may lead to race conditions between concurrent requests, so prefer the use of 'local' variables  

6  
--点号定义的，用点号来调用  
--冒号定义的，用冒号来调用  
--如function testModule.method2(...)，用testModule1.method2(111 , 222 , 333)来调用  
--如function testModule:method2(...)，用testModule1:method2(111 , 222 , 333)来调用  
--或function _M.new(self, width, height )，用local s1 = square:new(2, 3) － http://www.dahouduan.com/2017/12/07/lua-module-best-practice/  

7  
lua 参数默认值  
lua 的函数参数不支持默认值，可以通过间接的方式来实现  
```
function output(msg)
    msg = msg or "Hello"
    print(msg)
end 
```
