14.CountDownLatch, CyclicBarrier 和 Semaphore
20200911

1.CountDownLatch
	CountDownLatch countDownLatch = new CountDownLatch(6);

	子线程中 countDownLatch.countDown();

	主线程中 countDownLatch.await();

2.CyclicBarrier
	CyclicBarrier cyclicBarrier = new CyclicBarrier(7, 到7后执行的方法)

	子线程中 cyclicBarrier.await();

3.Semaphore
	信号量主要用于两个目的，一个是用于多个共享资源的互斥使用，另一个用于并发线程数的控制

	Semaphore semaphore = new Semaphore(3); //模拟3个停车位
	semaphore.acquire()
	semaphore.release()