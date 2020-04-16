# shell命令的基本操作

#### 设置在特定时间执行命令：
	at 13:00
	at> echo hello >>testFile
	at> echo world >>testFile 
	at> <EOT>
将会在13：00的时候执行将hello 和world输入到test File中去。可以设置其他命令。
设置完毕之后Ctrl+d 退出at指令(EOT)。
#### 循环命令
	for i in 1 2 4 8; do ./a.out $i >result$i; done;
设置不同的输入参数（1，2，4，8），将结果存在不同的result中。