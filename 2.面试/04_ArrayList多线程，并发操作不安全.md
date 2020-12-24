4.ArrayList多线程，并发操作不安全

20200907

```
(1)
在多线程环境下，调用某些方法并发争抢资源 （如add()）会引起错误 （ java.util.ConcurrentModificationException ）

(2)
解决方案:
	<1>用 new Vector();
	<2>用Collections.synchronizedList(new ArrayList());
	<3>用 new CopyOnWriteArrayList(); 读写分离，常用在读多写少时

	解决方案1和解决方案2性能不好，因为用了synchronized，是锁类的
	解决方案3，用了ReentrantLock, 是锁相关代码的，性能较好
```

(3)  
CopyOnWrite容器季写时复制的容器，往一个容器添加元素的时候，不直接往Object[]添加，而是先将当前容器Object[]进行Copy,复制出一个新的容器Object[] newElements, 然后新的容器Object[] newElements里添加元素，添加完元素后，再将原容器的引用指向新的容器 setArray(newElements); 这样做的好处是可以对CopyOnWrite容器进行并发的读，而不需要加锁，因为当前容器不会添加任何元素. 所以CopyOnWrite也是一种读写分离的思想，读和写不同的容器


v1-20201224