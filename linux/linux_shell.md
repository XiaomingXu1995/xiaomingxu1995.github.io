# Linux Shell 学习笔记
In the begining, shifting the input language methods between Chinese and English with `vim` is too hard. 
So the notebook is written in English for suiting the vim edit and input methods.


## 第一章 从这里开始，起飞了

### 注释和运行
* 脚本解释器
* 多行注释和单行注释
```bash
#/bin/bash 
<<COMMENT
Start the comment for multi-lines.
start with '<<COMMENT' 
end with 'COMMENT' keywords.
COMMENT
#this a comment line
```
* `bash test.sh` 开启子进程执行脚本
* `source test.sh` 直接在该线程下执行脚本
* `source` 和`.` 的功能一样

### 输出
* `echo -e "[31mOK\e0m"` 红色显示OK
* `echo -e "\033[3;10HOK"` 在第3行，第10列显示OK
* `printf "|%-10d|\n 12` 左对齐输出12
* `printf "|%10d|\n 12` 右对齐输出12

### 输入
* `read` 从标准输入读取一行数据
  * `-p` 显示提示信息
  * `-t` 设置读取数据的超时时间
  * `-n` 设置读取n个字符之后结束
  * `-r` 支持读取\,默认情况下\为转义字符
  * `-s` 静默模式，密码输入

### 重定向
* `&>> test.out` 将标准输出和错误输出都重定向到一个文件 
* `2>&1` 将错误输出重定向到标准输出
* `1>&2` 将标准输出重定向到错误输出

###
* 双引号和单引号可以引用一个整体
* 单引号可以屏蔽特殊符号`# $ `` \ * ~` 等
* 反引号使用命令的输出结果替代命令

### 变量
* `hello=123` 变量定义
* `echo {hello}` 变量使用
* `unset hello` 变量取消定义
* 常用变量
  * `$#` number of arguments, equivalently with `argc` in c++
  * `$1` the second argument, it must be `${n}` when n is larger than 9
  * `RANDOM` return a random integer in the 0-32767 range
  * `$$` return the PID of the current process
  * `$*` return all the arguments as an integration element
  * `$@` return all the arguments as individual elements

### filter of data and regular expression
* `grep` often with the Basic Ragular Expression
  * `-i` ignore case
  * `-v` inverse filter
  * `-w` filter the word
  * `-q` silent filter, not shown in screen

### Basic Regular Expression
* `c` char c
* `.` any single char
* `*` last char any times(can be 0 time)
* `.*` any char any time
* `[]` match any single char in the bracket
* `[x-y]` match continuous string range
* `^` match the begining of string
* `$` match the end of string
* `[^]` reverse match of the set in the bracket
* `\` match escape string
* `\{n,m\}` match last char repeat `n` times to `m` times
* `\{n,\}` match last char repeat at least `n` times
* `\{n\}` match last char repeat `n` times
* `\(\)` save the content between `\(` and `\)`, at most save 9 content ( used with `\n` )
* `\n` use the `\1` to `\9` to call the saved content by `\(\)`

### Extended Regular Expression
run with `grep -E` or `egrep` for Extended Regular Expresion
* `{n,m}` equivalent to `\{n,m\}` mention before
* `+` match last char once or many times
* `?` match last char any times (including none)
* `|` match the strings before or after `|`
* `()` match set as well as saving content, equivalent with `\(\)`

### arithmetic operation
For integer arithmetic operation
* `$((computation expression))`
* `$[computation expression]` 
* `let computation expresion`

For float operation
* `bc`
* `echo "obase=2; 11" |bc` change 11 from decimalism to binary
  * the default format is decimalism
  * `obase` is the output base format
  * `ibase` is the input base format

# Section 2 Artificial Intelligence Bash Script
## condition judgment 
**pay attention to the space between all the expressions and bracket**
* `[ expression ]` attention to the space near bracket
* `[ ! expression ]` negetion of expression
* `[[ expression ]]`
* `test` 
* `echo $?` can print the last quit state mask. `0` is `true`, others are `false`.
* `[ -z $TEST ] && echo Y || echo N` `-z` can test whether a string is null
* `[ -n $Jacob ] && echo Y || echo N` will print `Y` even though the `Jacob` is null since the `$Jacob` is considered as a space rather than null
* `[ -n "$Jacob" ] && echo Y || echo N` will print `N` and we should use `""` rather than `''` since `''` can mask the `$` and see it as an common char in the string

## comparison of integers
* `-eq` equal
* `-ne` not equal
* `-gt` greater than
* `-ge` greater than or equal
* `-lt` less than
* `-le` less or equal

## comparison of file 
all the description below return `true`
* `-e file` file or directory exists
* `-f file` file exists and is common file
* `-d file` directory exists
* `-b file` block device such as hard disk
* `-c file` char device such as keyboard or mouse
* `-L file` soft linked file
* `-p file` pipeline 
* `-r file` file exists and user has read authority
* `-w file` file exists and user has write authority
* `-x file` file exists and user has execute authority
* `-s file` file exists and not null
* `file1 -ef file2` file1 is same with file2
* `file1 -nt file2` file1 is newer than file2 or file1 exists while file2 does not exist
* `file1 -ot file2` file1 is older than file2 or file2 exists while file1 does not exist











