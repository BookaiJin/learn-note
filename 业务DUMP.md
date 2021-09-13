业务DUMP

```sequence
participant task
participant memManager
task -> memManager:init\nregister
note over memManager:task/thread-memObjInfo
task -> task:query
task -> memManager:collect
task -> task:expand
task -> memManager:collect
task -> task:html
```

问题：

1. 比较鸡肋，能统计计算对象大小的都是已知对象，已知了就不需要统计了，加上中止场景覆盖直接停止不就行了；



理想：

每一类gcroot作为根，选出最大的一条

1. 单拎出来线程内存大小，以线程作为gcroot，遍历线程上的对象大小，线程在计算过程中已经加了模板名；
2. 单拎出来静态变量/常量作为gcroot





```sequence
participant RunningTasks
participant SessionPool
participant SessionBeanList
participant Dumpoperation
participant disk
note over Dumpoperation:trigger
RunningTasks->Dumpoperation:collecte
SessionPool->Dumpoperation:collecte
Dumpoperation->SessionBeanList:generate
SessionBeanList->disk:serialize
Dumpoperation->disk:deserialize
note over Dumpoperation:restart
note over Dumpoperation:show all session info
```

