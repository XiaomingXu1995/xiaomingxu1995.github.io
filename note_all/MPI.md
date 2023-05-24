# MPI 的具体操作

具体问题可以参照: [`MPI-tutorial`](https://mpitutorial.com/tutorials/)

## MPICH的安装
MPICH的下载网站: [`download`](https://www.mpich.org/downloads/)
```bash
wget https://www.mpich.org/static/downloads/4.1.1/mpich-4.1.1.tar.gz
tar -xzvf mpich-4.1.1.tar.gz
mkdir ~/application/mpich-4.1.1
cd mpich-4.1.1 && ./configure --prefix=~/application/mpich-4.1.1 
# 如果configure failed， 看看具体报错信息，例如没有Fortran编译器之类的，根据提示--disable-fortran即可。
make -j && make install

# vim ~/.bashrc 使用绝对路径
export PATH=/home/user_home/xiaomingxu/application/mpich-4.1.1/bin:$PATH
export LD_LIBRARY_PATH=/home/user_home/xiaomingxu/application/mpich-4.1.1/lib:$LD_LIBRARY_PATH
```




