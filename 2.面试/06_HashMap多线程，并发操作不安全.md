6.HashMap多线程，并发操作不安全  
20200908

```
(1)  
在多线程环境下，调用某些方法并发争抢资源 （如put()）会引起错误 （ java.util.ConcurrentModificationException ）

(2)  
解决方案:  
	用ConcurrentHashMap
``

v1-20201224
