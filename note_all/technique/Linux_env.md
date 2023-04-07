# Linux 环境的各种操作

## Linux 查看动态链接库的位置
可以使用 `ldconfig` 工具来查找系统中安装的共享库的路径。
```bash
# 更新缓存
sudo ldconfig
ldconfig -p | grep <library_name>
```