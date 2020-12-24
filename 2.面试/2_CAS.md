2.CAS  
20200906   

1.CAS的全称为Compare-And-Swap, 它是一条CPU并发原语  
它的功能是判断内存某个位置的值是否为预期值，如果是则更改为新的值，这个过程是原子的  

  原子类（比如：AtomicInteger）的底层是用CAS实现

2.Unsafe类  
	Unsafe类是CAS的核心类可以直接操作特定内存的数据  

3.AtomicInteger中”value” variable -> 通过Unsafe取得内存地址 -> 再通过CAS对数据进行操作 ( 比较AtomicInteger中的值和通过内存地址取得的值，如果一样就对数据进行操作)  
  AtomicInteger.compareAndSet最终也是调用Unsafe中的CompareAndSwap实现

4.CAS的缺点  
	（1）do-while loop导致性能下降  
	（2）只能对单个共享变量保持原子操作 （对多个需要用synchronized）  
	（3）ABA问题  

5.ABA问题  
	step1:线程1读取A从主存到工作内存，线程2读取A从主存到工作内存  
	step2:线程2－修改A到B在工作内存，并更改主存A到B  
	step3:线程2－修改B到A在工作内存，并更改主存B到A  
	step4:线程1读取A,执行CAS操作，认为其没有修改过  

6.用AtomicStampedReference解决ABA问题  

v1-20201224
