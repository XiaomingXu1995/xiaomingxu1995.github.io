## Input and Output with High Performance
在很多应用实例中，虽然拥有良好的并行性，在多线程的时候会有相应的进程同步，有些在线程池中会有一些标准的输出，这些输出也许会成为程序最终的瓶颈。

#### `std::cout` VS `std::ofstream`
直接看下边这个样例：
```cpp
double t0 = get_sec();//get_sec()is from the program/c&c++;
for(int i = 0; i < 30000000; i++){
    std::cout << i << std::endl;
}
double t1 = get_sec();
std::cerr << "the time of std::cout is: " << std::endl;

std::ofstream outFile("test.txt");
for(int n = 0; n < 30000000;  n++){
    outFile << n;
    outFile << '\n';
    if(n % 30000 == 0)
        outFile.flush();
}
outFile.close();
double t2 = get_sec();
std::cerr << "the time of std::ofstream is: " << std::endl;
```
编译好之后执行 `./a.out > out` 命令，我们把最终的结果重定向到文件，得到最终两个结果，`std::cout` 将结果重定向到文件 `out.txt` 中，`std::ofstream` 将结果写入到 `test.txt` 中，结果MD5值相同。其中输出结果为：
```
the time of cout is: 31.9015s
the time of ofile is: 1.72658s
```

如果每次都执行 `flush()` 操作，两者的运行时间就会变成这样：
```
the time of cout is: 31.3951s
the time of ofile is: 31.3369s
```
可以看出在重定向到文件的时候 `flush()` 操作的占有时间。

