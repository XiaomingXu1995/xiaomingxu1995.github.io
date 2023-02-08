
## c&c++
有关c语言和c++的相关问题，其中有涉及到相关的技巧和代码规范。

* [代码规范和习惯](#代码规范和习惯)   
* [计时函数](#计时函数)   
* [有关编码的问题](#有关编码的问题)
* [函数指针](#函数指针)
* [标准库函数](#标准库函数)
* [调用shell命令](#c-调shell命令)
  
### 代码规范和习惯
* 变量和函数的命名要直观合理，不要模棱两可。
* 申请分配内存之后要记得释放，new配合delete， malloc配合free. 

### 计时函数
c++计时函数及使用样例。[参考手册](https://pubs.opengroup.org/onlinepubs/7908799/xsh/systime.h.html)

```cpp
#include <sys/time.h>
double get_sec(){
	struct timeval tv;
	gettimeofday(&tv, NULL);
	return (double)tv.tv_sec + (double)tv.tv_usec/1000000;
}
	
double t1 = get_sec();
//run the code needing to test
double t2 = get_sec();
std::cout << "the time of running the code is: " << t2 - t1 << std::endl;
```
### 有关编码的问题
c++或者c向输出流输出一些字符流，终端按照自己的编码方式查到对应的字符，将对应的字符显示出来，显示字体和字体库有关。[参考链接](https://www.zhihu.com/question/388125082/answer/1163293642)

Linux 终端默认utf-8解码，例如，“明”这个字的utf-8编码是：\xe6\x98\x8e，在 [Unicode Decoder](https://www.branah.com/unicode-converter) 上可以查询相关的字符解码。那么，可以有如下操作：
```cpp
//main.c
#include <stdio.h>

int main(){
	char arr[4] = {0xe6, 0x98, 0x8e, 0x00};//0x00 is byte array ending position.
	printf("%s\n", arr);
	return 0;
}
```
	$ gcc main.c -o main
	$ ./main
	$ 明

### 函数指针
函数指针指向某一种特定的函数，函数的输入参数类型和返回值类型确定，函数名不确定，例如：以下声明一个指向传入参数为两个`int`, 返回值为一个`int`的函数指针`func`。
```cpp
int (* func) (int, int);//declaration
int add(int a, int b){
	return a + b;
}
int sub(int a, int b){
	return a - b;
}

func = add;//assignment
func = sub;//assignment
```
声明函数`int (* func) (int, int)`中，`(* func)`代表这是一个函数指针，前边`int`表示该函数指针所指向函数的返回值为`int`类型，后边的`(int, int)`表示该函数指针所指向函数的传入参数类型。

**注意：`(* func)`的括号不可以省略，否则`int * func(int, int)`表示声明一个返回值为`int *`的函数，而非声明函数指针。**

### 标准库函数
c++有很多标准库函数，虽然在性能上可能会没有太多的优势，但是在功能上还是很不错的，而且很多标准库函数的性能比自己写的naive的函数还是要好一些的。
* [std::sort](http://www.cplusplus.com/reference/algorithm/sort/) 排序算法。
* [std::unordered_set](http://www.cplusplus.com/reference/unordered_set/unordered_set/) 维护一个集合，其中元素都是不重复的，支持快速哈希索引。
* [std::unordered_multiset](http://www.cplusplus.com/reference/unordered_set/unordered_multiset/) 维护一个集合，允许其中元素是重复的，支持快速哈希索引。
* [std::unordered_map](http://www.cplusplus.com/reference/unordered_map/unordered_map/) 维护一个`<key, T>`元素集合，其中元素的key值是不重复的，支持快速哈希索引。
* [std::unordered_multimap](http://www.cplusplus.com/reference/unordered_map/unordered_multimap/) 维护一个`<key, T>`元素集合，允许其中元素的key值是重复的，支持快速哈希索引。

### c++ 调shell命令
有时候需要在c++的代码中嵌入一些shell的命令操作，比如简单的文件合并 `cat` 命令等。在c++中调用shell命令需要关注一下[`<cstdlib>`中的`system`函数](http://www.cplusplus.com/reference/cstdlib/system/)

```cpp
#include <cstdlib>
#include <iostream>
using namespace std;

int main(){
	system("echo helloworld");
	string name1 = "1.txt";
	string name2 = "2.txt";
	system(("cat " + name1 + " >> result").c_str());
	system(("cat " + name2 + " >> result").c_str());
	return 0;
}
```
以上程序的运行结果会输出`helloworld`，并且会将文件`name1`和`name2`中的内容合并重定向到`result`文件中。

### c++ 函数参数使用引用
c++函数使用引用传递参数，保证传递的对象是同一个对象的引用，而不是再copy一个新的临时对象。有以下需求时需要传递引用：
* 该参数的值需要被修改，甚至时返回的主要参数，需要当作引用。
```cpp
// read the sketches from the inputFile
readSketches(vector<sketch_t> sketches, string inputFile); // cannot work, the sketches are only save in the temporary parameter object, 
readSketches(vector<sketch_t>& sketches, string intputFile); //works
```
* 该参数的对象所占用的内存较大，传递参数copy一份新的临时对象的时候，会产生一份新的内存开销。（参照RabbitKSSD中printInfo函数）
```cpp
// output the sketch infos to the outputFile
printInfo(vector<sketch_t> sketches, string outputFile); //It will copy a new sketches object, and used twice memory.
printInfo(vector<sketch_t>& sketches, string outputFile); //It will use the original object directly, without copy a new object and a new memory.
```