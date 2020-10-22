5.lua相关命令  
20201021

1.运行  
```
redis-cli --eval test.lua key1 key1
```

2.调试 
``` 
redis-cli --ldb --eval test.lua key1 key1
```
注意， 在使用 redis-cli 客户端的 -eval 选项的时候， 你可以将需要传递给脚本的键名以及参数一并提供给客户端， 其中键名和参数之间使用一个逗号来进行分割， 就像这样：
```
redis-cli --ldb --eval /tmp/script.lua mykey somekey , arg1 arg2
```
  
3.装入redis,并返回sha1 tag  
```
redis-cli script load "$(cat test.lua)"
```

4.同步模式  
```
redis-cli --ldb-sync-mode --eval /tmp/script.lua
```
注意， 运行在这一调试模式下的服务器在进行调试的过程中将不可用， 所以请小心使用这一选项。   
当处于这一模式时， abort 命令可以在中途停止那些已经对数据库进行过修改的脚本。 使用 abort 命令来终止调试会话与正常地终止调试会话是不同的： 如果用户只是简单地用 CTRL + C 来停止 redis-cli ， 那么调试会话将在整个脚本都执行完毕之后终止； 而 abort 则会中途停止脚本并在有需要时启动一个新的调试会话

5.Spring Boot中调用Lua  
脚本完成之后，添加到SpringBoot项目的resources目录下，即目录结构为：src/resources/person.lua。RedisTemplate提供两种方法可以执行Lua脚本

```
/**
    script为脚本资源，keys为一个数组形式的Key集合，最后为可选参数
*/
<T> T execute(RedisScript<T> script, List<K> keys, Object... args)

/**
    和上述中方式一致，多了两个参数，分别为参数序列化方法、结果序列化方法，更方便扩展
*/
<T> T execute(RedisScript<T> script, RedisSerializer<?> argsSerializer, RedisSerializer<T> resultSerializer, List<K> keys, Object... args)
```

DefaultScriptExecutor.eval()

从上面最后一个方法执行中可以看到，SpringBoot先计算了当前资源的Sha1，并使用EVALSHA指令尝试执行了一次，如果成功，则返回结果，如果缓存没有该脚本，则进入异常部分，并最终使用了EVAL指令进行执行。

从这里可以看到，SpringBoot客户端已经实现了脚本缓存的功能，只不过进行了封装，并且不对用户暴露。在使用时简单，傻瓜，并且用起来很舒服。总结一下就是：SpringBoot每次都先按EVALSHA执行，没有缓存脚本，再次执行EVAL，得到结果并缓存脚本
