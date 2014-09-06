#远程方法调用 (RMI)

####78.  什么是RMI ?
Java远程方法调用（RMI)是一个Java API，它执行的面向对象的等价远程过程调用（RPC）的方法，包括了直接传输序列化的Java类和分布式垃圾收集的支持。 远程方法调用（RMI），也可以看作是一个远程运行的对象上激活的方法的过程。RMI提供位置透明性，因为用户认为一个方法是在本地运行的对象上执行。 [RMI Tips here](http://www.javacodegeeks.com/2013/11/two-things-to-remember-when-using-java-rmi.html).

####79. 什么是RMI的体系结构的基本原理？
RMI的架构最重要的原则是将行为的定义和行为的实施分别对待。 RMI允许定义的行为和实现行为保持独立，并在独立的JVM中运行的代码。

####80. RMI的体系结构层是什么？
RMI的结构主要分为以下几层：
* 桩(Stub)和框架(Skeleton)层：该层位于开发者视图的下面。该层是负责拦截客户端请求接口的方法并重定向这些请求到远程RMI服务上。
* 远程引用层：架构的第二层是处理从客户端到服务器的远程对象引用的解析。该层解析并管理从客户端到远程服务对象的引用。该连接是一对一(单播)连接的。
* 传输层：该层主要负责连接参与服务的两个JVM。它基于通过网络连接的机子的TCP/IP，提供了基本的连通性，以及一些防火墙的渗透策略。

####81. 在RMI中远程接口的作用是什么？
远程接口用于识别那些不是来自本地机子接口但可以被调用的方法。所有对象都是必须直接或间接实现该接口的远程对象。实现该远程接口之前应该声明其远程接口，为每个远程对象定义构造方法，并在所有远程接口中为每个远程方法提供实现。

####82. java.rmi.Naming 类扮演的角色 ?
java.rmi.Naming类提供了存储和获取已注册的远程对象. Naming类中的每个方法都需要一个URL格式的String作为参数的名称.

####83. RMI中的绑定是什么意思 ?
绑定是关联或注册一个远程对象的名字的过程, 这个名字可以在以后用到, 用于查找与它绑定的远程对象. 远程对象可以通过Naming类中的bind或rebind方法与一个名字相关联.

####84. Naming 类中的bind与rebind方法的区别 ?
bind方法的绑定主要用于将特定的名字绑定到一个远程对象, 但rebind方法的绑定用于将特定的名字重新绑定到一个新的远程对象. 如果这个名字已经绑定过了, 使用rebind这个绑定会被替换.

####85. 运行RMI 程序的步骤?
为了使RMI程序正常运行需要以下步骤:
* 编译所有源文件.
* 用rmic生成stub.
* 启动rmiregistry.
* 启动RMIServer.
* 运行客户端程序.

####86.RMI中stub的角色 ?
远程对象的stub作为远程对象在本地程序中的表示或代理. 调用者调用本地stub的一个方法, 这个方法会在远程对象上执行.当一个stub的方法被调用时, 它经历了以下步骤:
* 初始化与运行远程对象的远程JVM的连接.
* 将参数编码并传递给远程JVM.
* 等待方法调用与执行的结果.
* 解码返回值或异常(如果执行失败).
* 将返回值返回给调用者.

####87. 什么是DGC？它是如何工作的？
DGC代表的是分布式垃圾收集。远程方法调用(RMI)使用的是DGC自动垃圾收集机制。由于RMI涉及到跨JVM的远程引用，垃圾回收就会相当困难。DGC使用相关的计数算法为远程对象提供自动存储管理。

####88. 在RMI中使用RMISecurityManager的目的是什么？
在RMI应用程序中可以使用RMISecurityManager提供安全管理器来下载代码。如果安全管理器没有设置好，RMI的类加载器不会从远程端下载任何类。

####89. 解释编组和解组。
当一个应用程序要通过网络来传送内存对象到另一台主机，或者保留它到存储器，内存表达法会将其转换到合适的格式。这个过程就叫做编组，而恢复操作就叫解组。

####90. 解释序列化和反序列化。
Java提供了一个机制，是指一个对象可以被表示为字节序列，包括对象的数据，以及对象类型的信息和存储在对象中的数据类型。因此，序列化可以看做是平面化对象为了存储到磁盘中，方便后面读取和重新配置的一种方式。反序列化是一种从平面化状态到活跃状态的一种转换对象的逆过程。