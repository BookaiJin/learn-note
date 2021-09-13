# tomcat

## tomcat-executor

使用了ThreadPoolExecutor，其中的阻塞队列实现了LinkedBlockingQueue

新增了：

### force

如果任务被reject，直接调用Queue的offer强制加入队列，增加Executors 的引用，用于调用Executors状态

因为我们知道ThreadPoo

