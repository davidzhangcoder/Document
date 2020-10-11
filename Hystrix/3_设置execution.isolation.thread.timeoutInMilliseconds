3.设置execution.isolation.thread.timeoutInMilliseconds
20201010

https://www.jianshu.com/p/b8d21248c9b1

这个超时时间要根据CommandKey所对应的业务和服务器所能承受的负载来设置，要根据CommandKey业务的平均响应时间设置，一般是大于平均响应时间的20%~100%,最好是根据压力测试结果来评估，这个值设置太大，会导致线程不够用而会导致太多的任务被fallback；设置太小，一些特殊的慢业务失败率提升，甚至会造成这个业务一直无法成功，在重试机制存在的情况下，反而会加重后端服务压力
