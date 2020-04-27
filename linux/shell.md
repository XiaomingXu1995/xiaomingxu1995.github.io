# shell命令的基本操作
很多命令都有官方手册，最官方的说明当然属于`man`。


* [设置在特定时间执行命令](#设置在特定时间执行命令)
* [循环命令](#循环命令)
* [迅速查找之前的命令](#迅速查找之前的命令)
* [time计时命令](#time计时命令)
* [文件的操作](#文件的操作)

#### 设置在特定时间执行命令：
	at 13:00
	at> echo hello >>testFile
	at> echo world >>testFile 
	at> <EOT>
	
将会在13：00的时候执行将hello 和world输入到test File中去。可以设置其他命令，例如设置在某个具体时间关机。
设置完毕之后Ctrl+d 退出at指令(EOT)。

#### 循环命令
	for i in 1 2 4 8; do ./a.out $i >result$i; done;
	
设置不同的输入参数（1，2，4，8），将结果存在不同的result中。

#### 迅速查找之前的命令
`Ctrl+r` 然后输入之前命令中的关键词就可以匹配到最近输入的完整命令。
如果匹配到的最近的完整指令不是所需要的，继续`Ctrl+r`直到匹配到所需指令。

#### time计时命令
`time ./a.out`列出运行程序`a.out`所用的时间。结果以标准错误流(standard error)输出，包括以下三个结果:
* real（从提交命令到终止命令所用的实际时间）
* user（用户程序所用的cpu时间）
* sys （系统调用所用的cpu时间）

注意，后两者是**cpu时间**，在某些情况下（例如多线程）会比real时间明显长，涉及程序优化等问题，real时间不单纯是后两者数据相加。

#### 文件的操作
* wc命令
  * `wc -l fileName` 查看文件有多少行
  * `wc -c fileName` 查看文件有多少字节
  * `wc -w fileName` 查看文件有多少字
* 查找文件位置命令
  * `find ./ -name "*hello.c"` 在当前目录下搜索`*hello.c`的位置。
* 查看文件大小命令
  * `df -lh` 查看磁盘剩余空间
  * `ls -lh hello.c` 查看`hello.c`文件的大小
  * `du -d 1 -lh .` 查看该目录下所有文件夹的大小以及该目录下所有文件总大小，`-d 1`表示文件夹层数为一层。

#### 管道命令
管道命令`command1|command2`中，`command1`的输出作为`command2`的输入，其中command1的输出为标准输出流，例如`lscpu | grep avx`
  
  