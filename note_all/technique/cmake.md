# cmake 的相关操作

## cmake 指定g++编译器没生效
如果你使用CMake指定g++编译器没有生效，可以尝试以下几种方法：

使用CMAKE_C_COMPILER和CMAKE_CXX_COMPILER变量指定编译器路径，例如：
```
cmake -DCMAKE_C_COMPILER=/usr/bin/gcc -DCMAKE_CXX_COMPILER=/usr/bin/g++ <path-to-source>
```

在CMakeLists.txt中添加以下语句：
```
set(CMAKE_C_COMPILER /usr/bin/gcc)
set(CMAKE_CXX_COMPILER /usr/bin/g++)
```