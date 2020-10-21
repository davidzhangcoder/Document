5.lua相关命令

1.运行  
```
redis-cli --eval test.lua key1 key1
```

2.调试 
``` 
redis-cli --ldb --eval test.lua key1 key1
```

3.装入redis,并返回sha1 tag  
```
redis-cli script load "$(cat test.lua)"
```