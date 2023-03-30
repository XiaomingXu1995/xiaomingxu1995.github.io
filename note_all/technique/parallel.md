# Parallel linux 下的并行神器

## install
linux gnu paralle 安装包的下载网址：http://ftp.gnu.org/gnu/parallel/
```bash
wget http://ftp.gnu.org/gnu/parallel/parallel-latest.tar.bz2
tar -xjvf parallel-latest.tar.bz2
cd parallel-latest
./configure --prefix=/home/user/application/parallel
make && make install
export PATH=/home/user/application/parallel/bin:$PATH

parallel -h
# you need to input 'will cite' to activate the parallel
```

## usage 
```bash
man parallel
cat arg.list | parallel ./main {}
```