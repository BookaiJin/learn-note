# ThreadPoolExecutor

流程图

```flow
st=>start: Start
opSubmit=>operation: Executor#submit(Runnable)
opExe=>operation: Runnable#run()
opReject=>operation: Executor is full, reject
opAddQueue=>operation: Queue add Worker
opNewThreadRun=>operation: new Worker(), (worker.thread = ThreadFactory.newThread(worker)).start()
condCore=>condition: workers.size() > corePoolSize
condQueue=>condition: workers.size() > queue.size()
condMax=>condition: workers.size() > maxPoolSize
condExecutorRunning=>condition: executor is running
e=>end
st->opSubmit->condCore
condCore(no)->opExe
condCore(yes)->opAddQueue
opAddQueue->condQueue
condQueue(yes)->condMax
condMax(no)->opNewThreadRun
opNewThreadRun->opExe
condQueue(no)->condExecutorRunning
condExecutorRunning(yes)->condMax
condExecutorRunning(no)->opReject
condMax(no)->opNewThreadRun
opNewThreadRun->opExe
condMax(yes)->opReject
opReject->e
opExe->e

```

![image-20210518093036858](/Users/bokai/Library/Application Support/typora-user-images/image-20210518093036858.png)

![image-20210518093100381](/Users/bokai/Library/Application Support/typora-user-images/image-20210518093100381.png)

线程状态的坑，放在更高层的dispather应该还好

价值

