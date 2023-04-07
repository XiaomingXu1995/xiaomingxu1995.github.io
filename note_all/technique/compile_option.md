# compiling options 如何设置编译选项

## 在使用 g++ 进行编译链接时，可以通过以下方式同时链接动态库和静态库：
在使用 g++ 进行编译链接时，可以通过以下方式同时链接动态库和静态库：
```
g++ -o output main.cpp -L/path/to/libs -lmy_static_lib -lmy_dynamic_lib
```
其中，-L 选项指定了静态库和动态库所在的路径，-l 选项分别指定了要链接的静态库和动态库的名称。请将 /path/to/libs 替换为你的库所在路径，my_static_lib 和 my_dynamic_lib 分别替换为静态库和动态库的名称。

请注意，如果同时链接了同一个函数的静态库和动态库，程序将会出现链接错误，因为函数在编译时会被重复定义。此时可以通过 -Wl,-Bstatic 和 -Wl,-Bdynamic 选项来指定链接静态库和动态库。例如：
```
g++ -o output main.cpp -L/path/to/libs -Wl,-Bstatic -lmy_static_lib -Wl,-Bdynamic -lmy_dynamic_lib
```
这里的 -Wl,-Bstatic 表示接下来要链接的库都是静态库，-Wl,-Bdynamic 表示接下来要链接的库都是动态库。