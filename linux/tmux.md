## tmux的基本操作

### 初等操作一
	tmux new -s hello 创建一个名为hello的终端
	Ctrl+b; d 退出该终端
	tmux a 启动最近的一个终端
	Ctrl+b; s 选择其他终端
	Ctrl+b; [ 允许滚屏，q 退出

### 初等操作二
	Ctrl+b; " 上下分屏，新开一个tmux终端界面
	Ctrl+b; % 左右分屏，新开一个tmux终端界面
	Ctrl+b; o 在上下或者左右分屏之间相互切换
	Ctrl+b; x 关闭其中一个分屏
	Ctrl+b; space 上下分屏和左右分屏互相转换	