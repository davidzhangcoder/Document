5.HashSet多线程，并发操作不安全  
20200908

```
(1)
在多线程环境下，调用某些方法并发争抢资源 （如add()）会引起错误 （ java.util.ConcurrentModificationException ）

(2)
解决方案:
	<1>用Collections.synchronizedSet(new HashSet());
	<2>用 new CopyOnWriteArraySet(); 读写分离，常用在读多写少时

CopyOnWriteArraySet底层是用CopyOnWriteArrayList实现

(3)
HashSet底层用HashMap实现，value用new Object()
```

v1-20201224