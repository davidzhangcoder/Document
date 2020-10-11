1.Hystrix
20200924

1.服务降级
	服务器忙，请稍后再试，不让客户端等待并立刻返回一个友好提示，fallback
	哪些情况会触发降级？
		程序运行异常
		超时
		服务熔断触发服务降级
		线程池／信号量打满也会导致服务降级

2.服务熔断(熔断后会尝试自己恢复－大流量熔断后，经过一段时间后，放一小部分流量过去，看能否正常工作，再到全面恢复)

	服务的降级 -> 进而熔断 -> 恢复调用链路

	(1).
	一旦调用服务方法失败并抛出了错误信息后，会自动调用@HyxtrixCommand标注好的	fallbackMethod调用类中的指定方法

	(2).
	在启动类中加入注解@EnableCircuitBreaker(对hysteria熔断机制的支持)

	(3)
	带来问题 方法数膨胀 和 高耦合
	在FeignClient中用FallbackFactory类解耦，在FallbackFactory中可以做 服务降级
	需要在yml中加入以下
		feign:
			hystrix:
				enabled: true