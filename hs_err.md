# hs_err 

## 流程

```sequence
participant crash
participant file
participant systemCheck
crash -> file:scan at 02:00
```



### 获取

位置：会漏一些

1. 工作目录「user.dir」
2. 临时目录「temp」
3. 如果拼接到了sout，fanruan.log或者catalina.out上，就丢了

### 时机

系统检查插件，每天夜里两点

#### 移动

移动文件到/WEB-INF/treasures/hs_err，改一下名字，后缀加上节点名

#### 解析

见下文

#### 解析结果

解析结果按照「时间-结果」表格保存在一个地方，/WEB-INF/assist/hs_err

#### 验证

调用系统检查插件判断项，项配置错误与解析结果相符，通知修改配置

| result         | config                |
| -------------- | --------------------- |
| OOM            | testPhysicalMem       |
| Jdk lambda bug | testJVMVersion        |
| lib mapping    | testmax_vm_map_count  |
| SIGBUG buffer  | testDisk              |
| SIGILL         | testFRversion         |
| 未知           | 统计os/jdk/容器版本？ |

#### 通知

上次宕机是由于XXXX，请修改。。。

未知，请发送崩溃报告/回传云端运维数据包分析

## 解析

怎么检测文件，是个大问题

按行读取按内容匹配

##### 已知信息

* 文件
  * 概要
    1. 概要原因
    2. jdk、jre版本、运行模式
  * 线程
    1. 崩溃线程、状态
    2. 代码
    3. 调用堆栈
  * 进程
    1. gc
    2. 映射
    3. 启动参数
    4. 变量
  * 系统
    1. 内存 空闲、使用
    2. 运行时长、生成时间



解析读文件

