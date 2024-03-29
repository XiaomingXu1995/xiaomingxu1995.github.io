# vim 的相关操作
vim有两种模式，编辑模式和非编辑模式，通过**Esc键**在两种模式之间相互切换达到熟练的运用。

## 进入编辑模式
	i 从光标之前编辑
	a 从光标之后编辑
	o 从下一行的位置编辑

## 非编辑模式下的相关操作

#### 光标定位
	h j k l 移动光标
	gg 回到文件顶端
	G 回到文件底端
	$ (shift+4) 定位光标到行尾
	^ (shift+6) 定位光标到行首
	% (shift+5) 定位到括号匹配处
	* (shift+8) 查找高亮定位光标所在单词，n 定位下一个，N 定位上一个。
	Ctrl + f 向下滚屏一页
	Ctrl + b 向上滚屏一页

#### 缩进
	= 设置自动缩进（gg = G 全文自动缩进； 1 = 10 前10行自动缩进）

#### 折叠与展开
	zf 12 从当前行折叠之后的12行
	zf % 折叠括号匹配（折叠某个函数）
	zo 将某个折叠展开（vimdiff相同的行会折叠，可以zo展开折叠）
	
#### 剪切复制粘贴
	yy 复制一行
	yaw 复制一个单词
	10yy 复制10行
	dd 剪切一行
	daw 剪切一个单词
	10dd 剪切10行
	x 剪切一个字符
	p 在光标之后粘贴（如果复制的是整行，那么保留行缩进）

#### 自定义选中范围
	v 设置选中范围(可以配合光标定位使用：v; G; 表示选中当前光标到文件结尾)
	shift+v 整行选中
	Ctrl+v 整列选中（对于代码多行加注释：Ctrl+v；shift+insert; EscEsc)

#### 查找和替换
	/hello 高亮文件中所有的hello，n跳转下一个，N跳转上一个
	:%s /int/long/g 将文件中所有的int替换成long
	:s /int/long/g 将该行中所有的int替换成long

#### 高级操作
	:%normal jdd 删除奇数或者偶数行（normal:普通模式；j:下移一行；dd删除一行）

#### 自动补全，撤销恢复
	Ctrl+p 自动补全最近的匹配词。
	u 撤销之前的操作
	Ctrl+r 恢复之前的操作

#### 屏幕显示
	Ctrl+s 终止屏幕显示（不是卡了，操作有效果，只是没显示出来）
	Ctrl+q 退出终止屏显
	Ctrl+z 挂起vim进程，回到shell界面，通过fg调出vim挂起进程
	jobs 查看挂起的vim进程，可能有多个挂起进程，jobs有相应编号id
	fg 调出最近挂起vim进程，多个挂起时fg id 启动相应编号的进程

#### 打开多个文件
	:vsp fileName 竖直分屏，在左侧新打开一个文件
	:sp fileName 水平分屏，在上侧新打开一个文件
	Ctrl w w 在同时打开的多个文件之间进行光标切换
	:vertical resize +10 将当前分屏加宽10(适用于左右分屏)

#### 比较两个文件的不同
	vimdiff file1 file2 同时打开两个文件并显示其不同

需要注意：当两个文件比较大的时候，在两个文件差异较大的时候，`vimdiff`两个文件可能会崩溃，建议先查看MD5值，如果不相同，建议使用`diff file1 file2 >out`,如果发现两个文件差距不大，再使用`vimdiff`。

## 设置vim相关属性
临时的设置可以输入冒号+指令，长期设置修改根目录下的.vimrc文件。

	set nu 设置行号
	set autoindent 设置自动缩进
	set hlsearch 设置高亮搜索
	set ts=4 设置tab键为4个空格
	
## vim非正常关闭.swp文件的处理
vim打开文件的时候因为断电等非正常关闭之后，会产生一个相应的swp文件。比如：`vim main.c` 非正常关闭，会再同目录下产生一个`.main.c.swp`隐藏文件（通过`ls -a`可以查看），里面包含关闭时相关的文件信息。如果当时没有保存，可以通过`vim -r main.c` 打开文件，就会恢复到之前编辑的状态，然后`:wq`保存退出，删除`.main.c.swp`文件即可。
























