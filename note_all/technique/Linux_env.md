# Linux 环境的各种操作

- [Linux 查看动态链接库的位置](#dynamic-lib)
- [yum 查找某个软件包](#yum)
- [Linux systemctl](#systemctl)
- [Linux ulimit](#ulimit)

## Linux 查看动态链接库的位置 {#dynamic-lib}
可以使用 `ldconfig` 工具来查找系统中安装的共享库的路径。
```bash
# 更新缓存
sudo ldconfig
ldconfig -p | grep <library_name>
```

## yum 查找某个软件包 {#yum}
在 CentOS 或者其他基于 RPM 的 Linux 发行版中，您可以使用 `yum search` 命令来查找软件包。该命令会在 CentOS 官方仓库以及您已经配置的其他仓库中搜索软件包名称及其描述。例如，要查找名为 libomp 的软件包，您可以在终端中输入以下命令：
```
yum search libomp
```

## libomp-devel.i686中的i686是什么意思 
在 Linux 中，i686 表示 Intel 32 位体系结构（也称为 IA-32 或 x86）。它是 Intel 8086 处理器的后继者，它支持 IA-32 指令集，可以运行在 32 位模式下。

在 RPM 软件包管理器中，i686 表示针对 i686 架构的 32 位二进制软件包。相应地，x86_64 表示针对 x86_64 架构的 64 位二进制软件包。例如，在 CentOS 和 Fedora 等 RPM-based 的 Linux 发行版中，`libomp-devel.i686` 表示针对 32 位系统的 OpenMP 开发库软件包，可以在 32 位系统上使用。

## --with-gmp、--with-mpfr 和 --with-mpc  分别是什么库
具体来说，它们分别对应以下库：

* GMP（GNU Multiple Precision Arithmetic Library）：用于高精度整数和有理数计算。
* MPFR（Multiple Precision Floating-Point Reliable Library）：用于高精度浮点数计算。
* MPC（Multiple Precision Complex Library）：用于高精度复数计算。

这些库都是用 C 语言编写的，并且提供了一组 API，可以在程序中进行调用。

在编译 GCC 时，这些库会被用于生成 GCC 本身以及编译过程中所需要的各种工具和库。因此，在编译 GCC 时，需要确保这些库已经正确安装，并且在配置选项中指定了它们的正确路径。

注意，如果这些库已经安装在系统的默认路径中，则不需要使用 `--with-gmp`、`--with-mpfr` 和 `--with-mpc` 选项。否则，您需要将这些选项设置为库的正确安装路径。

## 如何在编译gcc源码的时候，保留静态数学库和静态c库
在编译 GCC 时，如果需要保留静态数学库和静态 C 库，可以使用以下配置选项：
```
--enable-static --disable-shared --with-mpfr=<path-to-mpfr> --with-gmp=<path-to-gmp> --with-mpc=<path-to-mpc>
```
其中：

* --enable-static：启用静态库。
* --disable-shared：禁用共享库。
* --with-mpfr=<path-to-mpfr>：指定 MPFR 数学库的安装路径。
* --with-gmp=<path-to-gmp>：指定 GMP 数学库的安装路径。
* --with-mpc=<path-to-mpc>：指定 MPC 数学库的安装路径。

您可以根据实际情况修改 <path-to-mpfr>、<path-to-gmp> 和 <path-to-mpc> 为正确的库安装路径。

需要注意的是，如果使用这些选项进行编译，生成的 GCC 可执行文件将只能链接到静态库，不能链接到共享库。如果需要链接到共享库，可以省略 `--disable-shared` 选项。

## 源码编译gcc 没有libc.a libm.a
在源码编译 GCC 时，如果您想要得到静态链接的 libc 和 libm 库，可以通过在配置 GCC 时指定 `--enable-static-libgcc` 和 `--enable-static-libstdc++` 参数来实现。

运行 configure 脚本来配置 GCC，例如：
```
../configure --prefix=/usr/local/gcc --enable-static --enable-shared --enable-languages=c,c++ --enable-static-libgcc --enable-static-libstdc++
make && make install
```
其中，--prefix 参数指定 GCC 的安装目录，--enable-static 参数指定启用静态链接，--enable-shared 参数指定启用动态链接，--enable-languages 参数指定编译支持的语言，--enable-static-libgcc 参数指定启用静态链接的 libgcc 库，--enable-static-libstdc++ 参数指定启用静态链接的 libstdc++ 库。

需要注意的是，在某些发行版中，libc 和 libm 静态链接库可能不是默认安装的，您可能需要手动安装它们。

## gcc 10.1.0 应该配合哪个版本的glibc

根据GCC 10.1.0官方文档，它支持的最低glibc版本为2.17。因此，如果你想在GCC 10.1.0下编译使用glibc的程序，建议使用glibc 2.17或更高版本。同时，建议使用与GCC版本匹配的glibc版本以获得最佳兼容性和性能。

根据GCC官方文档，GCC 10.1.0 建议搭配 Glibc 2.31 及以上版本使用。您可以通过以下命令查看您系统中已安装的Glibc版本：
```
ldd --version
```

## Linux systemctl {#systemctl}
systemctl 是一个用于管理系统服务的命令行工具，用于控制 systemd 系统和服务管理器。以下是一些常用的 systemctl 命令：

* 启动一个服务：systemctl start service_name
* 停止一个服务：systemctl stop service_name
* 重启一个服务：systemctl restart service_name
* 显示一个服务的状态：systemctl status service_name
* 开机自启一个服务：systemctl enable service_name
* 禁止一个服务开机自启：systemctl disable service_name
* 查看一个服务是否已开机自启：systemctl is-enabled service_name
* 查看一个服务是否正在运行：systemctl is-active service_name
* 查看所有已启动的服务：systemctl list-units --type=service
* 查看所有已启动的服务及其详细信息：systemctl list-units --type=service --all

除了上述命令之外，systemctl 还有许多其他命令，包括 mask、unmask、isolate、kill、show 等等。可以通过 man systemctl 命令查看详细的帮助信息。

## ulimit -a 命令的各项输出表示什么意思 {#ulimit}
ulimit -a 命令会显示当前 shell 会话中所有限制的值，包括软限制和硬限制。下面是 ulimit -a 命令的输出示例以及各项输出的含义：
```
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 24235
max locked memory       (kbytes, -l) 65536
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024  # 文件描述符的软限制和硬限制
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) unlimited
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```
下面是各项输出的含义：
* core file size: 指定内核转储(core dump)文件的最大大小（以块为单位）。
* data seg size: 指定进程数据段的最大大小（以千字节为单位）。
* scheduling priority: 指定进程调度优先级。
* file size: 指定进程创建的文件的最大大小（以块为单位）。
* pending signals: 指定进程能够排队等待接收的最大信号数。
* max locked memory: 指定进程能够锁定的最大内存量（以千字节为单位）。
* max memory size: 指定进程可用的最大物理内存量（以千字节为单位）。
* open files: 指定进程能够同时打开的最大文件数。这里的输出包括了软限制和硬限制，其中软限制是当前限制的值，而硬限制是进程能够设置的最大限制值。
* pipe size: 指定进程创建的管道的最大大小（以字节为单位）。
* POSIX message queues: 指定进程可用的 POSIX 消息队列的最大总字节数。
* real-time priority: 指定进程的实时调度优先级。
* stack size: 指定进程堆栈的最大大小（以千字节为单位）。
* cpu time: 指定进程能够使用的 CPU 时间的最大数量（以秒为单位）。
* max user processes: 指定一个用户能够同时运行的最大进程数。
* virtual memory: 指定进程可用的最大虚拟内存量（以千字节为单位）。
* file locks: 指定进程能够锁定的最大文件数。