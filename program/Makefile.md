## Makefile的相关规则
Makefile的基本规则只有两点：
* 依赖
* 时间戳

理解好Makefile的工作原理，需要了解一些编译和链接的内容，建议去阅读《程序员的自我修养——链接、装载与库》。
### 基本假设：
源文件为 `hello.cpp main.cpp hello.h`，main.cpp 中调用hello.cpp的函数。
### version 1
```
1:  main: main.o hello.o
2:      g++ main.o hello.o -o main
3:  main.o: main.cpp 
4:      g++ -c main.cpp -o main.o
5:  hello.o: hello.c
6:      g++ -c hello.c -o main.o
```
基本规则1：依赖关系
* `main: main.o hello.o` 表示最终形成的目标文件`main`依赖于`main.o`和`hello.o`，即`目标文件：依赖文件1 依赖文件2`
* `g++ main.o hello.o -o main `将`main.o`和`hello.o`链接成最终可执行文件`main`。这一行就是通过编译或者链接命令通过所依赖的文件生成目标文件，要注意这一行之前是需要加`Tab`键才有效。
* 第4行中的-c表示只编译当前文件而不链接成最终可执行文件。

基本规则2：时间戳
* 上边的各个命令会执行，只要存在以下几种情况之一：
  * 生成文件的时间戳早于依赖文件（例如：在生成main.o之后又修改了main.cpp,`g++ -c main.cpp -o main.o`会在make的时候执行。
  * 还没有生成所需要的生成文件。（例如：hello.o文件还没有生成）
  * 每一个生成文件的时间戳都是最新的，执行make指令的时候，会提示`nothing to be done, main is update to date.`等等。
  
### version 2