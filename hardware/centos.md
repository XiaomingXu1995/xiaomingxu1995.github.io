## 安装centos 系统

#### 下载系统镜像
下载系统镜像我一般从中科大的镜像网站下载。下载版本为[8.1.1911](https://mirrors.ustc.edu.cn/centos/8.1.1911/isos/x86_64/)

#### 制作启动盘
这个系统镜像刻完了不到8G，8GU盘估计够用（我用的是32G的）。

制作启动盘有坑，Windows下普通的刻盘工具（UltraISO)刻的盘会有问题，在引导的时候不能正常引导，报错 `dracut-initqueue timeout` 。


如果刻盘工具选择有误，网上说的方法诸如：修改U盘标签和修改启动菜单等，但是并不管用。
至于这个针对[UltraISO的教程](https://www.jianshu.com/p/e3cd90c540c3)我没有仔细去尝试，感兴趣的可以尝试。


我直接下载了官方的刻盘工具：[Fedora Media Writer](https://getfedora.org/zh_CN/workstation/download/)
这个建议来自于这个朋友的[经验分享](https://blog.csdn.net/ywd1992/article/details/79849654)，我之所以选择他的建议直接格式化重新刻盘的原因是，他的经历和我一样，尝试了几种其他的教程，得出一个重要的结论：
**没 神 么 软 用** ,干脆直接用新的刻盘工具重新刻盘。


#### 安装
引导成功了之后，安装过程基本上就是无脑的下一步了。其中也有一些注意事项，可以参考具体的[Linux中国的教程](https://zhuanlan.zhihu.com/p/85807189)。其中的磁盘分区我选择`Automatic`形式，教程中是`Custom`形式。


至此，安装完毕。

#### 之后U盘不识别
用`Fedora Media Writer`写入的系统启动盘再次插入电脑上不识别，解铃还须系铃人，再次通过`Fedora Media Writer`重新格式化U盘即可。