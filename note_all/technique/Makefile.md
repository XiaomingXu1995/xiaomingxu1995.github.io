# Makefile 的撰写规则与指南

## Makefile 如何写
Makefile 是一种用于构建和管理软件项目的工具，通常用于自动化构建、编译、测试和打包等操作。下面是一些编写 Makefile 的基本步骤：

定义变量：定义一些常用的变量，比如编译器名称、编译选项等。

定义规则：定义规则，指定源文件和目标文件之间的依赖关系，以及构建目标文件所需的命令。

定义目标：定义 Makefile 的默认目标以及其他目标，比如编译、测试、打包等。

添加注释：为了方便维护和理解，可以添加一些注释来解释每个变量和规则的作用和用法。

下面是一个简单的 Makefile 示例：
```
CC=gcc
CFLAGS=-Wall -O2
LDFLAGS=-lm

all: myprog

myprog: main.o utils.o
	$(CC) $(CFLAGS) $(LDFLAGS) $^ -o $@

main.o: main.c utils.h
	$(CC) $(CFLAGS) -c $< -o $@

utils.o: utils.c utils.h
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f *.o myprog
```
在这个 Makefile 中，我们定义了三个变量，CC 用于指定编译器名称，CFLAGS 用于指定编译选项，LDFLAGS 用于指定链接选项。然后我们定义了三个规则，分别是构建 myprog 目标所需的规则，main.o 目标所需的规则，以及 utils.o 目标所需的规则。最后我们定义了一个 clean 目标，用于删除生成的目标文件。

要执行 Makefile，只需要在命令行中输入 make 命令即可。如果要执行特定的目标，可以输入 `make <target>` 命令，比如 make clean。

### Makefile 中 `$,%, $@, $<, $^ =, :=` 分别代表什么
在 Makefile 中，`$、%、$@、$< 和 $^` 等符号是 Makefile 的内置变量和函数，用于指定文件、目录、命令等内容。它们的具体含义如下：

* $：表示变量引用的符号，用于引用变量的值。
* %：表示通配符，用于匹配文件名中的任意字符。
* $@：表示目标文件，用于指定 Makefile 规则中的目标文件。
* $<：表示依赖文件列表中的第一个依赖文件，用于指定 Makefile 规则中的依赖文件。
* $^：表示依赖文件列表，用于指定 Makefile 规则中的所有依赖文件。
* =：是 Makefile 的变量赋值符号，用于将一个变量赋值为一个表达式，其中表达式中的变量会被展开为它们的值。
* :=：是 Makefile 的即时展开符号，用于将一个变量赋值为一个表达式，其中表达式中的变量会被立即展开为它们的值。

下面是一个示例，展示了如何在 Makefile 中使用这些符号：
```
CFLAGS := -I./include
OBJDIR := obj
SRCDIR := src
SRCFILES := $(wildcard $(SRCDIR)/*.c)
OBJFILES := $(patsubst $(SRCDIR)/%.c,$(OBJDIR)/%.o,$(SRCFILES))

all: myprogram

myprogram: $(OBJFILES)
    gcc -o $@ $^

$(OBJDIR)/%.o: $(SRCDIR)/%.c
    gcc $(CFLAGS) -c $< -o $@
```
在这个示例中，`$@、$< 和 $^` 分别用于指定目标文件、依赖文件和所有依赖文件列表。`= 和 := `用于将变量 `CFLAGS、OBJDIR、SRCFILES 和 OBJFILES` 赋值为不同的表达式。`%` 则用于匹配文件名中的任意字符。

## Makefile 如何简写所有的.c编译成相应的.o
可以使用 Makefile 中的自动变量和隐式规则来简化编译所有的 .c 文件成相应的 .o 文件。下面是一个示例 Makefile：
```
CC=gcc
CFLAGS=-Wall -O2

# 定义目标，默认构建 all
all: myprog

# 定义 myprog 目标，依赖于所有的 .o 文件
myprog: $(patsubst %.c, %.o, $(wildcard *.c))
	$(CC) $(CFLAGS) $^ -o $@

# 隐式规则，将所有的 .c 文件编译成相应的 .o 文件
%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

# 定义 clean 目标，用于清理生成的目标文件和可执行文件
clean:
	rm -f *.o myprog
```
在这个 Makefile 中，我们使用了自动变量 $<，表示规则中的第一个依赖项，即对应的 .c 文件，同时使用了通配符 * 和函数 wildcard 和 patsubst 来自动生成所有的 .c 和 .o 文件的文件名。然后，我们定义了一个隐式规则，将所有的 .c 文件编译成相应的 .o 文件。最后，我们定义了一个 clean 目标，用于删除生成的目标文件和可执行文件。

使用这个 Makefile，只需要在命令行中输入 make 命令即可自动编译所有的 .c 文件成相应的 .o 文件，并构建可执行文件 myprog。

### Makefile中patsubst 是干什么的
patsubst 是 Makefile 中的一个函数，用于将一组模式字符串中的模式部分替换为另一个字符串。具体来说，它的语法如下：
```
$(patsubst pattern,replacement,text)
```
其中，pattern 表示需要匹配的模式字符串，可以包含通配符 %；replacement 表示替换后的字符串；text 表示需要进行替换的原始字符串。patsubst 函数会将 text 中所有匹配 pattern 的部分替换为 replacement，并返回替换后的结果。

在 Makefile 中，patsubst 函数通常用于处理文件名或路径名，比如将一组 .c 文件名转换成相应的 .o 文件名。例如，如果我们有一组 .c 文件名，如 foo.c bar.c baz.c，我们可以使用以下语句将它们转换成相应的 .o 文件名：
```
OBJS = $(patsubst %.c, %.o, foo.c bar.c baz.c)
```

### Makefile 中wildcard 是干什么的
wildcard 是 Makefile 中的一个函数，用于获取当前目录下满足一定模式的所有文件名。具体来说，它的语法如下：
```
$(wildcard pattern)
```
其中，pattern 表示需要匹配的模式字符串，可以包含通配符 * 和 ?，用于匹配任意字符或任意单个字符。wildcard 函数会返回满足 pattern 模式的所有文件名，以空格分隔。如果没有匹配的文件，返回空字符串。

在 Makefile 中，wildcard 函数通常用于获取需要编译的源文件列表，比如获取所有的 .c 文件。例如，我们可以使用以下语句获取当前目录下所有的 .c 文件名：
```
SRCS := $(wildcard *.c)
```
这样，变量 SRCS 就包含了当前目录下所有的 .c 文件名，以空格分隔。如果需要获取 src 目录下所有的 .c 文件，可以使用以下语句：
```
SRCS := $(wildcard src/*.c)
```
除了使用 wildcard 函数，我们也可以使用其它方式获取文件列表，例如使用 find 命令获取指定目录下的所有文件，再使用 grep 命令筛选出 .c 文件。例如，以下语句可以获取 src 目录下所有的 .c 文件：
```
SRCS := $(shell find src -type f -name "*.c" | grep -v '/\.' | sort)
```
这样，变量 SRCS 就包含了 src 目录下所有的 .c 文件名，以空格分隔。其中，find 命令用于获取指定目录下所有的文件，-type f 表示只获取普通文件，-name "*.c" 表示只获取后缀名为 .c 的文件。grep -v '/\.' 命令用于排除隐藏文件，sort 命令用于对文件名进行排序。最终得到的结果是一个按照文件名排序的 .c 文件列表。

### Make file 如何打印变量
在 Makefile 中，可以使用 $(info) 函数打印变量的值。具体来说，$(info) 函数用于输出一个字符串到标准输出，该字符串可以包含 Makefile 变量、函数等。语法如下：
```
$(info string)
```
其中，string 表示需要输出的字符串，可以包含 Makefile 变量和函数，用于输出变量的值、函数的返回值等。当 Makefile 执行到 $(info) 函数时，会在标准输出中输出 string 的值。

例如，我们可以使用以下语句打印变量 SRCS 的值：
```
$(info SRCS=$(SRCS))
```
注意，$ 后边的变量要用括号括起来。








