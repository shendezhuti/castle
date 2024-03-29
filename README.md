# castle
城堡游戏-学习设计原则 castle game-learn design principle

# 消除代码复制

程序中存在相似甚至相同的代码块，是非常低级的代码质量问题。

代码复制存在的问题是，如果需要修改一个副本，那么就必须同时修改所有其他的副本，否则就 存在不一致的问题。这增加了维护程序员的工作量，而且存在造成错误的潜在危险。很可能发 生的一种情况是，维护程序员看到一个副本被修改好了，就以为所有要修改的地方都已经改好 了。因为没有任何明显迹象可以表明另外还有一份一样的副本代码存在，所以很可能会遗漏还 没被修改的地方。

我们从消除代码复制开始。消除代码复制的两个基本手段，就是函数和父类。

# 封装-用封装降低耦合

要评判某些设计比其他的设计优秀，就得定义一些在类的设计中重要的术语，以用来讨论设计的优劣。对于类的设计来说，有两个核心术语：耦合和聚合。 耦合这个词指的是类和类之间的联系。之前的章节中提到过，程序设计的目标是一系列通 过定义明确的接口通信来协同工作的类。耦合度反映了这些类联系的紧密度。我们努力要获得低的耦合度，或者叫作松耦合（loose coupling）。

耦合度决定修改应用程序的容易程度。在一个紧耦合的结构中，对一个类的修改也会导致对其他一些类的修改。这是要努力避免的，否则，一点小小的改变就可能使整个应用程序发生改变。另外，要想找到所有需要修改的地方，并一一加以修改，却是一件既困难又费时的事情。 另一方面，在一个松耦合的系统中，常常可以修改一个类，但同时不会修改其他类，而且整个程序还可以正常运作。

本周会讨论紧耦合和松耦合的例子。 聚合与程序中一个单独的单元所承担的任务的数量和种类相对应有关，它是针对类或方法 这样大小的程序单元而言的理想情况下，一个代码单元应该负责一个聚合的任务（也就是说，一个任务可以被看作是 一个逻辑单元）。一个方法应该实现一个逻辑操作，而一个类应该代表一定类型的实体。聚合 理论背后的要点是重用：如果一个方法或类是只负责一件定义明确的事情，那么就很有可能在另外不同的上下文环境中使用。遵循这个理论的一个额外的好处是，当程序某部分的代码需要改变时，在某个代码单元中很可能会找到所有需要改变的相关代码段。

- 可以运行的代码！=良好的代码
- 对代码做维护的时候最能看出代码的质量
- Room类和Game类都有大量的代码和出口相关
- 尤其改之前的代码Game类大量使用了Room成员变量 
- 简单的说，类和类的关系称作耦合，耦合度越低越好，保持距离是形成良好代码的关键

# 可扩展性

我们已经实现的设计与其原始版本比较已经有了很大的改进，然而还可以有进一步的提高。 优秀的软件设计者的一个素质就是有预见性。什么是可能会改变的？什么是可以假设在软件的生命期内不会改变的？ 在游戏的很多类中硬编码进去的一个假设是，这个游戏会是一个基于字符界面的游戏，通过终端进行输入输出，会永远是这样子吗？ 以后如果给这个游戏加上图形用户界面，加上菜单、按钮和图像，也是很有意思的一种扩 展。如果这样的话，就不必再在终端上打印输出任何文字信息。还是可能保留着命令字，还是会在玩家输入帮助命令的时候显示命令字帮助文本，但是可能是显示在窗口的文字域中，而不是使用System.out.println？

可扩展性的意思就是代码的某些部分不需要经过修改就能适应将来可能的变化

#用接口来实现聚合

- 给Room类实现的新方法，把方向的细节彻底隐藏在了Room类内部
- 今后方向如何实现就和外部无关

# 用容器来实现灵活性

- Room的方向是用成员变量表示的，增加或者减少方向就要改变代码

- 如果用Hash来表示方向，那么方向就不是“硬编码”的了



#以框架+数据来提供可扩展性

- 从程序中识别出框架和数据，以代码实现框架，将部分功能以数据的方式加载，这样能在很大程度上实现可扩展性。
- 命令的解析是否可以脱离if-else
- 定义一个Handerl来处理命令
- **用Hash表来保存命令和Handler之间的关系**（这个是之前没见到的用法，受益很大）


