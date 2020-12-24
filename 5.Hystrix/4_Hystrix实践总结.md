4.Hystrix实践总结  
20201029  

1  
配在Server端( OrderServiceImpl.java中 )在FallBack方法中要抛出异常，不然不会回滚

2  
在Zuul上配熔断，限流和降级的Performance要好于配在 OrderServiceImpl.java中的方法上

3  
TPS = 请求数 / 时间  

	jmeter聚合报告中，Throughput是用来衡量请求的吞吐量，也就是tps，tps=样本数/运行时间

	jmeter的Throughput = (number of requests) / (total time) ，即Throughput =(sample样本数)/(最后一个线程启动的时间+最后一个线程持续的时间-第一个线程启动的时间)

	吞吐量与并发数
		一个接口一秒钟能承受50个并发，不代表可以有50个吞吐量；
		吞吐量与系统性能息息相关；
		设置长时间跑接口，比如1秒50并发，持续60秒——发现实际接口请求数1461个，时间60秒，TPS参数较稳定；
		TPS大概在23左右，所以当前这个接口，系统能处理的事务在23个左右
		TPS=请求数/时间

* 在Jmeter中不断提高并发压测数，得到较合理的Avg时间
* 用Throughput＋20%设为Hystrix的coresize
* queuesize设为和coresize一样
* timeout为Avg时间+50%
  
  
* 一般系统要 TPS 30
* 较好点的要 TPS 50
* 秒杀要 TPS 100 或 TPS 200

4  
调优时需要注意：  
* Hystrix 线程池  
* Zuul 线程池 (Hystrix)  
* Zuul 连接池 (HttpClient)  
* Tomcat 连接池  
* Redis 连接池  
* 数据库 连接池  
* MySql Server 线程池 (如使用MySql数据库)  

5.超时  
(1)
* Ribbon
* Hystrix
* 如把Hystrix配的比Ribbon小，会提示warn(出于Ribbon重试考虑)
* 如把Ribbon重试配成0,那么Hystrix可以配的比Ribbon小  
(2)
* Hystrix - threadpool: coresize和maximumSize的坑

6  
Hystrix configures in application.yml, either set it for all Feign clients or for each method

can not set it on a class by class basis
