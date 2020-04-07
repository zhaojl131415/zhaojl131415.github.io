---
title:      JDK性能调优监控工具
date:       2019-08-14 15:32
author:     "zhaojl131415"
catalog:    true
categories: 
    - Java
    - JVM
tags:
    - Java
    - JVM
---

# JVM性能调优监控工具
## Jinfo
查看正在运行的Java程序的扩展参数
### 查看JVM的参数
![](/img/jvm/tune/1574240991013-0789fcee-7f1f-4851-bb43-395738a13b43.png)
### 查看java系统属性
等同于System.getProperties()
![](/img/jvm/tune/1574240995655-3842bf59-02af-47d9-b0e9-baa24b7ac725.png)
## Jstat
jstat命令可以查看堆内存各部分的使用量，以及加载类的数量。

命令格式：jstat [-命令选项] [vmid] [间隔时间/毫秒] [查询次数]
### 类加载统计
`jstat -class 进程id`
- Loaded：加载class的数量
- Bytes：所占用空间大小
- Unloaded：未加载数量
- Bytes：未加载占用空间
- Time：时间
### 垃圾回收统计
`jstat -gc 进程id`
- S0C：第一个Survivor区的空间
- S1C：第二个Survivor区的空间
- S0U：第一个Survivor区的使用空间
- S1U：第二个Survivor区的使用空间
- EC：Eden区的总空间
- EU：Eden区的使用空间
- OC：Old区的总空间
- OU：Old区的已使用空间
- MC：元空间的总空间
- MU：元空间的使用空间
- CCSC：压缩类的总空间
- CCSU：压缩类的使用空间
- YGC：年轻代垃圾回收次数
- YGCT：年轻代垃圾回收消耗时间
- FGC：老年代垃圾回收次数
- FGCT：老年代垃圾回收消耗时间
- GCT：垃圾回收消耗总时间
### 堆内存统计
`jstat -gccapacity 进程id`
- NGCMN：新生代最小空间
- NGCMX：新生代最大空间
- NGC：当前新生代空间
- S0C：第一个Survivor区空间
- S1C：第二个Survivor区空间
- EC：Eden区的总空间
- OGCMN：老年代最小空间
- OGCMX：老年代最大空间
- OGC：当前老年代空间
- OC：当前老年代空间
- MCMN：最小元空间大小
- MCMX：最大元空间大小
- MC：当前元空间大小
- CCSMN：最小压缩类空间大小
- CCSMX：最大压缩类空间大小
- CCSC：当前压缩类空间大小
- YGC：年轻代GC次数
- FGC：老年代GC次数
### 新生代垃圾回收统计
`jstat -gcnew 进程id`
- S0C：第一个Survivor区空间
- S1C：第二个Survivor区空间
- S0U：第一个Survivor区的使用空间
- S1U：第二个Survivor区的使用空间
- TT：对象在新生代存活的次数
- MTT：对象在新生代存活的最大次数
- DSS：期望Survivor区大小
- EC：Eden区的空间
- EU：Eden区的使用空间
- YGC：年轻代垃圾回收次数
- YGCT：年轻代垃圾回收消耗时间
### 新生代内存统计
`jstat -gcnewcapacity 进程id`
- NGCMN：新生代最小空间
- NGCMX：新生代最大空间
- NGC：当前新生代空间
- S0CMX：最大第一个Survivor区空间
- S0C：当前第一个Survivor区空间
- S1CMX：最大第二个Survivor区空间
- S1C：当前第二个Survivor区空间
- ECMX：最大Eden区空间
- EC：当前Eden区空间
- YGC：年轻代垃圾回收次数
- FGC：老年代垃圾回收次数
### 老年代垃圾回收统计
`jstat -gcold 进程id`
- MC：元空间的总空间
- MU：元空间的使用空间
- CCSC：压缩类的总空间
- CCSU：压缩类的使用空间
- OC：Old区的总空间
- OU：Old区的已使用空间
- YGC：年轻代GC次数
- FGC：老年代GC次数
- FGCT：老年代垃圾回收消耗时间
- GCT：垃圾回收消耗总时间
### 老年代内存统计
`jstat -gcoldcapacity 进程id`
- OGCMN：老年代最小空间
- OGCMX：老年代最大空间
- OGC：当前老年代空间
- OC：当前老年代空间
- YGC：年轻代GC次数
- FGC：老年代GC次数
- FGCT：老年代垃圾回收消耗时间
- GCT：垃圾回收消耗总时间
### 元空间内存统计
`jstat -gcmetacapacity 进程id`
- MCMN：最小元空间大小
- MCMX：最大元空间大小
- MC：当前元空间大小
- CCSMN：最小压缩类空间大小
- CCSMX：最大压缩类空间大小
- CCSC：当前压缩类空间大小
- YGC：年轻代GC次数
- FGC：老年代GC次数
- FGCT：老年代垃圾回收消耗时间
- GCT：垃圾回收消耗总时间
### 总垃圾回收统计
`jstat -gcutil 进程id`
- S0：第一个Survivor区当前使用比例
- S1：第二个Survivor区当前使用比例
- E：Eden区使用比例
- O：Old区使用比例
- M：元空间使用比例
- CCS：压缩使用比例
- YGC：年轻代垃圾回收次数
- FGC：老年代垃圾回收次数
- FGCT：老年代垃圾回收消耗时间
- GCT：垃圾回收消耗总时间
## Jmap
可以用来查看内存信息
### 堆的对象统计
jmap -histo 7824 > xxx.txt

如图：

![](/img/jvm/tune/1574241015826-9dd6919b-ceb2-4e1d-9270-238495e9b2cc.png)

- Num：序号
- Instances：实例数量
- Bytes：占用空间大小
- Class Name：类名
### 堆信息
![](/img/jvm/tune/1574241023464-f79385b0-0a96-4e8f-be90-abff7562028e.png)
### 堆内存dump
![](/img/jvm/tune/1574241028133-06b67eb0-56a0-4f6f-8745-13a8d3de48a0.png)

jmap -dump:format=b,file=temp.hprof

也可以在设置内存溢出的时候自动导出dump文件（项目内存很大的时候，可能会导不出来）

1.-XX:+HeapDumpOnOutOfMemoryError

2.-XX:HeapDumpPath=输出路径

-Xms10m -Xmx10m -XX:+PrintGCDetails -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=d:\oomdump.dump
![](/img/jvm/tune/1574241045813-247c52cc-2ba0-44ab-8509-d496c060b190.png)

可以使用jvisualvm命令工具导入文件分析
![](/img/jvm/tune/1574241278584-e443d518-0e51-4992-83ad-354c6f7c4aa6.png)
## Jstack
jstack用于生成java虚拟机当前时刻的线程快照。
![](/img/jvm/tune/1574241287753-cbfa44e2-4338-4de6-9ece-71d6ee1e2d9d.png)
# 调优
JVM调优主要就是调整下面两个指标

停顿时间：垃圾收集器做垃圾回收中断应用执行的时间。-XX:MaxGCPauseMillis

吞吐量：垃圾收集的时间和总时间的占比：1/(1+n),吞吐量为1-1/(1+n)。-XX:GCTimeRatio=n
## GC调优步骤
1.打印GC日志

`-XX:+PrintGCDetails -XX:+PrintGCTimeStamps -XX:+PrintGCDateStamps -Xloggc:./gc.log`

Tomcat可以直接加载JAVA_OPTS变量里

2.分析日志得到关键性指标

3.分析GC原因，调优JVM参数
### 1.Parallel Scavenge收集器(默认)
分析parallel-gc.log
第一次调优，设置Metaspace大小：增大元空间大小-XX:MetaspaceSize=64M  -XX:MaxMetaspaceSize=64M
第二次调优，增大年轻代动态扩容增量（默认是20%），可以减少YGC：-XX:YoungGenerationSizeIncrement=30
比较下几次调优效果：

吞吐量 | 最大停顿 | 平均停顿 | YGC | FGC | 
-|-|-|-|-|
97.467% | 370 ms | 50.0 ms | 16 | 2 |
98.9% | 110 ms | 32.5 ms | 12 | 0 |


### 2.配置CMS收集器
-XX:+UseConcMarkSweepGC
分析gc-cms.log
### 3.配置G1收集器
-XX:+UseG1GC
分析gc-g1.log
young GC:[GC pause (G1 Evacuation Pause)(young)
initial-mark:[GC pause  (Metadata GC Threshold)(young)(initial-mark) (参数：InitiatingHeapOccupancyPercent)
mixed GC:[GC pause (G1 Evacuation Pause)(Mixed) (参数：G1HeapWastePercent)
full GC:[Full GC (Allocation Failure)(无可用region)
（G1内部，前面提到的混合GC是非常重要的释放内存机制，它避免了G1出现Region没有可用的情况，否则就会触发 FullGC事件。CMS、Parallel、Serial GC都需要通过Full GC去压缩老年代并在这个过程中扫描整个老年代。G1的Full GC算法和Serial GC收集器完全一致。当一个Full GC发生时，整个Java堆执行一个完整的压缩，这样确保了最大的空余内存可用。G1的Full GC是一个单线程，它可能引起一个长时间的停顿时间，G1的设计目标是减少Full GC，满足应用性能目标。）
查看发生MixedGC的阈值：jinfo -flag InitiatingHeapOccupancyPercent 进程ID
调优：
第一次调优，设置Metaspace大小：增大元空间大小-XX:MetaspaceSize=64M  -XX:MaxMetaspaceSize=64M
第二次调优，添加吞吐量和停顿时间参数：-XX:GCTimeRatio=99 -XX:MaxGCPauseMillis=10
## GC常用参数
### 堆栈设置
- -Xss:每个线程的栈大小
- -Xms:初始堆大小，默认物理内存的1/64
- -Xmx:最大堆大小，默认物理内存的1/4
- -Xmn:新生代大小
- -XX:NewSize:设置新生代初始大小
- -XX:NewRatio:默认2表示新生代占年老代的1/2，占整个堆内存的1/3。
- -XX:SurvivorRatio:默认8表示一个survivor区占用1/8的Eden内存，即1/10的新生代内存。
- -XX:MetaspaceSize:设置元空间大小
- -XX:MaxMetaspaceSize:设置元空间最大允许大小，默认不受限制，JVM Metaspace会进行动态扩展。
### 垃圾回收统计信息
- -XX:+PrintGC
- -XX:+PrintGCDetails
- -XX:+PrintGCTimeStamps
- -Xloggc:filename
### 收集器设置
- -XX:+UseSerialGC:设置串行收集器
- -XX:+UseParallelGC:设置并行收集器
- -XX:+UseParallelOldGC:老年代使用并行回收收集器
- -XX:+UseParNewGC:在新生代使用并行收集器
- -XX:+UseParalledlOldGC:设置并行老年代收集器
- -XX:+UseConcMarkSweepGC:设置CMS并发收集器
- -XX:+UseG1GC:设置G1收集器
- -XX:ParallelGCThreads:设置用于垃圾回收的线程数
### 并行收集器设置
- -XX:ParallelGCThreads:设置并行收集器收集时使用的CPU数。并行收集线程数。
- -XX:MaxGCPauseMillis:设置并行收集最大暂停时间
- -XX:GCTimeRatio:设置垃圾回收时间占程序运行时间的百分比。公式为1/(1+n)
### CMS收集器设置
- -XX:+UseConcMarkSweepGC:设置CMS并发收集器
- -XX:+CMSIncrementalMode:设置为增量模式。适用于单CPU情况。
- -XX:ParallelGCThreads:设置并发收集器新生代收集方式为并行收集时，使用的CPU数。并行收集线程数。
- -XX:CMSFullGCsBeforeCompaction:设定进行多少次CMS垃圾回收后，进行一次内存压缩
- -XX:+CMSClassUnloadingEnabled:允许对类元数据进行回收
- -XX:UseCMSInitiatingOccupancyOnly:表示只在到达阀值的时候，才进行CMS回收
- -XX:+CMSIncrementalMode:设置为增量模式。适用于单CPU情况
- -XX:ParallelCMSThreads:设定CMS的线程数量
- -XX:CMSInitiatingOccupancyFraction:设置CMS收集器在老年代空间被使用多少后触发
- -XX:+UseCMSCompactAtFullCollection:设置CMS收集器在完成垃圾收集后是否要进行一次内存碎片的整理
### G1收集器设置
- -XX:+UseG1GC:使用G1收集器
- -XX:ParallelGCThreads:指定GC工作的线程数量
- -XX:G1HeapRegionSize:指定分区大小(1MB~32MB，且必须是2的幂)，默认将整堆划分为2048个分区
- -XX:GCTimeRatio:吞吐量大小，0-100的整数(默认9)，值为n则系统将花费不超过1/(1+n)的时间用于垃圾收集
- -XX:MaxGCPauseMillis:目标暂停时间(默认200ms)
- -XX:G1NewSizePercent:新生代内存初始空间(默认整堆5%)
- -XX:G1MaxNewSizePercent:新生代内存最大空间
- -XX:TargetSurvivorRatio:Survivor填充容量(默认50%)
- -XX:MaxTenuringThreshold:最大任期阈值(默认15)
- -XX:InitiatingHeapOccupancyPercen:老年代占用空间超过整堆比IHOP阈值(默认45%),超过则执行混合收集
- -XX:G1HeapWastePercent:堆废物百分比(默认5%)
- -XX:G1MixedGCCountTarget:参数混合周期的最大总次数(默认8)

进程物理内存远大于Xmx的问题分析
https://www.cnblogs.com/duanxz/p/6148534.html