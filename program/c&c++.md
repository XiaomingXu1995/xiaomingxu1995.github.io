## c&c++
有关c语言和c++的相关问题，其中有涉及到相关的技巧和代码规范。

### 代码规范和习惯
    变量和函数的命名要直观合理，不要模棱两可。
    申请分配内存之后要记得释放，new配合delete， malloc配合free.
	
### 计时函数
	//c++计时函数
	
	```c
	
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

