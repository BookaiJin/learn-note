# Java内存模型

## 乐观锁CAS同步

```sequence
title:AtomicInteger为例
participant thread1
participant main mem
participant thread2
note over thread1:工作内存中value=1
note over thread2:工作内存中value=1
thread1 -> main mem:incrAndGet
thread2 -> main mem:incrAndGet
```

