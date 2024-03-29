# ParNew垃圾回收器

ParNew实际上是Serial的并行版本，除了ParNew采用多线程进行垃圾回收之外，其他的和Serial基本一直，ParNew在Serial之上也没有太多的创新。 但是它是确是
不少运行在服务端模式下的HotSpot虚拟机，尤其在JDK7之前的遗留系统中，它是首选的新生代垃圾回收器，其中有一个与功能与性能无关的原因是：除了Serial以外，
目前只有ParNew能与CMS配合工作。

在JDK5版本时，HostSpot推出了一款具有跨时代意义的老年代垃圾回收器“CMS”，它是一款真正意义上的并发垃圾回收器，能让用户线程和垃圾回收线程同时工作，
遗憾的是它作为JDK1.5新出的虚拟机，它无法与Parallel Scavenge配合工作，所以在JDK5时，老年代时使用CMS垃圾收集器，新生代只能使用Serial或者ParNew
垃圾收集器。ParNew也是在使用CMS的默认新生代垃圾收集器。

可以说是CMS的出现才巩固了ParNew的地位，不过成也萧何败也萧何，随着垃圾收集器的不断发展，更先进的G1垃圾收集器带着CMS的继承者和替代者的光环登场，G1是
一个面向全堆的收集器，不需要新生代垃圾收集器的配合使用，所以从JDK9开始，ParNew加CMS收集器的组合就不被官方推荐的服务端模式下的收集器解决方案了，官方
希望它能够被G1所替代，甚至取消了ParNew与Serial Old的组合以及Serial和CMS的组合，这意味着也只有CMS可以和ParNew配合使用了。所以也可以理解ParNew
并入了CMS垃圾收集器。

ParNew在单核CPU的环境中绝对不会比Serial有更好的性能，因为存在线程交互的开销。但是在多核处理器的情况下，ParNew还是比Serial的效果要好很多。