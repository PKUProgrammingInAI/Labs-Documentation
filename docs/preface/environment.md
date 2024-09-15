# 环境配置
?> 或许这会是你们最想在文档里看到的一个东西? 

正所谓有句话说得好, 万事开头难. 对于写项目的开发者来说, 开头的事就是要配环境. "工欲善其事, 则必先利其器". 一个好的环境十分珍贵, 应该让同志们先配. 想想助教我去年选课时候都是摸着石头过河, 一把辛酸泪啊T_T

在课程文档中, 我会根据我去年的经验, 提供 Windows 平台和 WSL 下的配置步骤. 

!> 本篇的前提是你的电脑要有不那么旧的 Nvidia 独立显卡, 集成显卡和 AMD 显卡不适用于本教程, 请和助教联系在机房完成实验. 

!> 助教自身的经验表明, windows 环境下真的非常不推荐使用 Windows 环境下配置 CUDA 环境. (都是血和泪)

?> 请在确保达成以上条件后再往下看

## 我们需要什么?
- `CUDAToolkit`工具链
- `CMake`或者是别的支持CUDA的构建工具(当然visual studio也可以)
- 一个`python`环境, 版本可以自己来定.

如果以上的东西你都会自己准备, 那么恭喜你, 这一节不需要看了×

> 有的同学可能会问: 助教助教, 既然配环境要做很多工作, 而且还有杂七杂八的问题, 那为啥不用 Docker 呢, 你做一个镜像我们直接拉取就行, 都不用自己配
> 很不幸的是, 不同电脑上的CUDA版本不一, 助教也无法保证一个版本的CUDAToolkit能在所有的机器上都兼容, 因此我们需要同学们自己来配这个环境. 
> - 一方面, 相信在这篇文档的帮助下, 配好环境并不是一件很难的事, 毕竟去年我们还是自己摸索的呢.
> - 另一方面, 这个过程也能锻炼你们一些作为开发者的基本素养. 
## Windows 平台
?> 这助教怎么嘴上说着不要身体却很诚实, 明明说不推荐用 Windows 却还是出了教程...

咳, 当然我只是提供教程而已, 实际上在哪里进行实验不还是看你们自己么(×)

在终端或者命令提示符 cmd 中, 如果你运行`nvidia-smi`, 会看到如下结果:
```
$ PS C:\Windows\System32> nvidia-smi
Sun Sep 15 23:05:12 2024
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 560.94                 Driver Version: 560.94         CUDA Version: 12.6     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                  Driver-Model | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 3060 ...  WDDM  |   00000000:01:00.0  On |                  N/A |
| N/A   48C    P8             17W /  130W |    1634MiB /   6144MiB |     26%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+
...
```
这里的`CUDA Version`就代表了你的 Nvidia 显卡的 CUDA 版本, 我这里是12.6, 你们的可能会更高, 也可能会更低, 取决于机器新旧. 

于是, 你就可以在[这里](https://developer.nvidia.com/cuda-toolkit-archive)寻找你需要的对应版本的 CUDAToolkit, 然后下载安装就可以了.

安装之后请在终端或者命令提示符里输入`nvcc --version`
```
$ PS C:\Windows\System32> nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2022 NVIDIA Corporation
Built on Wed_Sep_21_10:41:10_Pacific_Daylight_Time_2022
Cuda compilation tools, release 11.8, V11.8.89
Build cuda_11.8.r11.8/compiler.31833905_0
```
出现上面类似的就算成功了.

实际上, 我的cuda工具链已经很久没有更新过了, 反而是中间显卡驱动更新了好几次, 顺带着把支持的CUDA版本也抬高了, 才会出现目前两个版本对不上的情况, 但是不要紧, 如果实在不兼容再换也是没问题的.

然后你需要一个构建工具, 为什么需要呢, 我们且先按下不表, 配好就是.

这里推荐大家使用`CMake`, 它本身是一个跨平台的构建工具, 而且在很早就支持了CUDA项目的构建.

在 Windows 上直接到[这里](https://cmake.org/download/)下载就可以, 记得需要下Binary distributions(二进制分发), 并且选对对应的平台. 

完事之后在终端输入`cmake --version`
```
$ PS C:\Windows\System32> cmake --version
cmake version 3.25.1

CMake suite maintained and supported by Kitware (kitware.com/cmake).
```
这就ok了.

未完待续...