## vectorization
有关向量化的基本操作以及注意事项。

#### 向量化指令
相应的向量化指令参考[intel intrinsics guide](https://software.intel.com/sites/landingpage/IntrinsicsGuide/)。

* 有些指令函数参数中包含立即数，包括`permute`或者`shuffle`指令，这个立即数不可以时变量，因为要在编译时能够确定该参数。（`const`常量可以）。

#### 相应的环境要求

* 运用相应的指令的时候，要查看他的**CPU FLAGS**，然后通过`lscpu`或者`cat /proc/cpuinfo`查看自己的机器是否支持该**CPU FLAGS**.

#### 编译器

* 不同的编译器对应不同的指令。向量化的指令主要参考Intel指令，所以**intrinsic guide**中的指令对于Intel的编译器`icc`和`icpc`只要机器满足其**CPU FLAGS**就可以正常编译使用。但是对于`gcc`和`g++`编译器，某些函数可能在`gcc`的头文件中并没有声明，比如某些`load`函数或者`abs`指令。这个时候需要寻找相应的同功能替代指令。比如`loadu_si512`替代`loadu_epi64`,异或操作代替`abs`指令。

#### CPU指令

#### 头文件