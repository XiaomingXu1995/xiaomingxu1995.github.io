# all technique including the environment of Linux, the hardware and software recommendation, the website.

## [Linux parallel](./technique/parallel.md)
## [Git](./technique/git.md) 
## [Linux_env](./technique/Linux_env.md)
## [cmake](./technique/cmake.md)
## [compile_option](./technique/compile_option.md)
## [Makefile](./technique/Makefile.md)
## [proxy](./technique/proxy.md)

## Linux 操作

### vim 代码跳转
安装一个`ctags`, 在代码路径中构建ctags index, 可以实现代码之间的跳转。
```bash
# instal ctags
sudo yum install ctags

# generate ctags index
ctags -R ./src/*

# open the main.cpp
vim src/main.cpp
# jump into the implementation of the function
# press Ctrl + ]
# jump back to the calling place
# press Ctrl + t

```

### 测试硬盘速度
```bash
# 清理系统缓存（需要root权限）
sudo echo 1 > /proc/sys/vm/drop_caches

# 测试硬盘读写速度
sync; dd if=/dev/zero of=./hello.out bs=4M count=1024; sync #write
dd if=./hello.out of=/dev/null bs=4M #read, need to drop_cache
```


## ssh 

[sshd man website](http://man.openbsd.org/sshd)





