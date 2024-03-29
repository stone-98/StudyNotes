# Serial/Serial old垃圾收集器

Serial垃圾收集器是最基础、历史最悠久的收集器，曾经是HotSpot虚拟机新生代收集器的唯一选择。Serial Old 就是Serial 的老年代产品。

Serial顾名思义它是一个单线程的垃圾收集器，这里的单线程并不仅仅是说它只会利用一个线程去完成它的工作，重在而是它进行工作时将会暂停用户线程。

Serial和Serial Old的区别就是Serial用于回收新生代、Serial Old用于回收老年代，并且Serial采用复制算法、Serial采用标记i整理算法。

下面示意了Serial和Serial old收集器的运行过程：

![image-20230716133059454](https://cxyzyw-site.oss-cn-beijing.aliyuncs.com/images202307161345822.png)

从JDK1.3开始，HoSpot虚拟机开发团队一直为了消除或者降低用户线程因垃圾收集器而导致停顿一直努力，从Serial收集器到Parallel再到CMS和G1，以至到现在的ZGC等，我们了解到用户线程暂停的时间越来越短，但是现在仍然无法完全消除。

到这里，你可能觉得Serial现在完全没有用武之地了，然而事实并非如此，它依然是HotSpot虚拟机运行在客户端模式下默认的新生代收集器，它也有它的优势，那就是简单并且高效（与其他收集器的单线程相比）。对于内存资源受限的情况下，它是所有收集器里额外消耗内存最小的，对于单核处理器或者处理器不多的情况下，Serial由于没有线程交互的开销，专心做垃圾收集自然可以获得更高的单线程收集效率。对于桌面应用程序来说，一般分配给Java虚拟机的内存并不会太大，收集几十兆乃至几百兆的新生代，垃圾收集器的停顿随时间完全可以控制在几十毫秒内，这点暂停时间对于用户是完全可以接受的，所以Serial收集器在客户端应用程序是一个很好的选择。
