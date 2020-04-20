## c&c++
有关c语言和c++的相关问题，其中有涉及到相关的技巧和代码规范。

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
#include <stdio.h>

int main(){
	char arr[4] = {0xe6, 0x98, 0x8e, 0x00};//0x00 is byte array ending position.
	printf("%s\n", arr);
	return 0;
}
```
上面运行结果就会在终端输出汉字“明” 。