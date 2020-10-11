2.Hystrix - 错误：java.lang.RuntimeException：could not acquire a semaphore for execution
20201002

https://blog.csdn.net/weixin_41231928/article/details/105238389

默认10个线程，当然第11个就报错，于是配置文件增加下面的配置：
hystrix.threadpool.default.coreSize=100 hystrix.threadpool.default.maxQueueSize=1500 hystrix.threadpool.default.queueSizeRejectionThreshold=1000 hystrix.command.default.execution.timeout.enabled=false hystrix.command.default.execution.isolation.strategy=THREAD
