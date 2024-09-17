# 一些前置知识和你可能会用到的东西
本课程将会用到如下的一些知识:
- CUDA编程
- 并行算法
- 将CUDA和C代码封装成能被python调用的形式
- 在python中编写自动微分和优化器的代码
- 分布式计算(Maybe Optional?)
这样, 你就收获了一个可以进行炼丹的深度学习框架. 

## CUDA编程
关于CUDA编程, 这是我们课上要讲的重点, 因此助教在这里不做赘述, 请同学们认真听课并复习课件.

这里有一些链接你可能会用到: 
- [Nvidia官方开发者论坛](https://forums.developer.nvidia.com/), 里面会有一些常见问题的解答. 
- [Nvidia官方手册](https://www.nvidia.cn/docs/IO/51635/NVIDIA_CUDA_Programming_Guide_1.1_chs.pdf), 这是Nvidia CUDA编程的官方文档, 可以进行一些函数接口的查阅.
- [HPC wiki的CUDA编程入门](https://hpcwiki.io/gpu/cuda/), 这是HPC wiki的CUDA编程入门教程, 作者也是去年选课的一位大佬, 目前在信科大四(大家应该会听说过他).

## 并行算法
这部分比较偏理论, 但是如果仔细推导下来会发现一点都不难, 这也是课上要讲的重点, 同样不做赘述.

## 跨语言相关
很多同学可能会疑惑: 我这门课需要用到CUDA C和python, 我之前写过的项目要么是纯C/C++, 要么是纯python或者别的, 总之都是一种语言, 那这个课程项目需要同时用 CUDA C 和 python , 该怎么写?项目组织又该是什么样的呢?

?> 这段是助教自己的理解, 也是为了帮助同学们好理解而这样描述.

事实上, 我们可以这样思考: 不同的语言内部运作是不同的, 但我们不关心他的细节, 我们只需要让他向外界表现的东西是一样的, 那么他内部是什么东西就无关紧要. 我们可以用这种**向外界表现一样的东西**来进行交流. 这样的东西叫做**接口**(Interface). 这样的思想非常常见, 也非常重要. 比如著名的计算机科学家 David Wheeler 曾经说过:
> All problems in computer science can be solved by another level of indirection.  
> 在计算机科学中, 所有的问题都可以通过增加一层抽象来解决.

这里的抽象, 实际上和接口是近义词, 主旨思想就是屏蔽内部细节, 增加外部接口.

有一个术语描述了这样的一种需求: FFI(Foreign Function Interface), 翻译过来就是语言交互接口, 允许我们在一种语言中编写函数, 在另一种语言中调用.
> 事实上, 熟悉 python 的同学们可能知道 python 本身效率极低, 但是 torch 和 numpy 这种库效率却奇高无比, 实际上他们底层就是用 c 编写的, 然后暴露出了接口供 python 调用. 

?> 除了 FFI 以外, 还有很多方式可以进行语言间的交互, 比如命令行接口和 HTTP 接口, 但是效率会比 FFI 低一些(因为同样进行了抽象, 而且层数更多), 好处是更加灵活(这个接口你可以自己去定义转换的方法).  
这部分也是助教根据自己的经验写的(毕竟这一块属于经验之谈), 如果不对也请勘误.

### 如何进行python对C/C++的调用?
#### 对C的调用

?> 这是助教推荐的方式

[这个链接](https://docs.python.org/zh-cn/3.12/library/ctypes.html)是 python 的官方文档, 里面是对 ctypes 用法的解释. 这个库可以读取c语言编译成的 dll(dynamic-link libraries, 动态链接库)并暴露出 python 接口供 python 代码调用.它同时规定了 c 语言中的数据类型在 python 中以何种方式表现. 动态链接库和静态链接库也是大多数语言进行 FFI 的主要形式.

如果嫌太长看不下去, 也可以看看PythonCookbook的[教程](https://python3-cookbook.readthedocs.io/zh-cn/latest/c15/p01_access_ccode_using_ctypes.html), 相对更好吃一些(

本课程中, 我们需要实现自己的 Tensor 类, 助教建议:
- 将你的 Tensor 类用 python 实现
- 在c中编写一些基础函数
- 然后在 python 的 Tensor 类中调用不同的基础函数实现不同的功能.

TODO...