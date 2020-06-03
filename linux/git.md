## git 的相关操作
git 的相关操作在这里应该是最基本的操作的，因为这个网站就是在GitHub上的。要熟悉本地git和远程GitHub之间的相互关系和git的基本规则。


#### 基本操作：clone 
`git clone` 命令是将远程的相关的文件下载到自己的本地目录下。执行以下命令就会将`xiaomingxu1995.github.io`文件夹下载到你当前目录下，并且里面会有相应的`.git`文件夹(通过`ls -a`查看）保留当前git信息。
```
git clone git@github.com:XiaomingXu1995/xiaomingxu1995.github.io.git
```
#### 基本操作：add，commit，push
在个人单机器独自开发的时候，这三个是在本地修改并提交到远程的最基本操作。
* git add file.c 是将本地修改之后的文件file.c添加到git目标中。
* git commit -m "update file.c" 是将本次修改提交并添加comment信息。
* git push -u origin master 是将该次提交推到远程GitHub上去。
  
如果是多人协作更新一个Repository，或者多台电脑更新就会出现新的问题。这个时候需要一些新的命令。



#### 基本操作：pull
`git pull` 命令是将远程的修改更新到本地，要求本地相对于远程没有修改（如果有，则需要进行merge操作）。如果远程修改的文件和本地修改的文件不是同一个文件，可以直接pull。如果远程修改的文件和本地修改的文件有冲突(修改的是同一个文件)，那么尽量选择手动merge，自动merge会出现部分代码出现两遍，而且带有相关的修改信息，整体代码显示非常乱。

* 为了避免上述merge操作，尽量在修改代码之前先pull一下，将远程的修改提前同步到本地，从而规避merge操作。
* 如果是多人协同工作的话，尽量协商好不修改同样的文件，如果有修改，手动merge的时候要非常小心。

#### 基本操作：log
`git log` 命令是用来查看git的相关commit记录，每次commit都有自己独自的commit ID，可以用来查看本地的commit记录。当进行`git pull` 操作之后会将远程的commit记录同步到本地。如果你的本地文件相对于本地的commit没有进行过修改，就可以正常的进行pull操作，无论本地的commit记录与远程相比相差几条。

#### 基本操作：checkout
`git checkout file.c` 命令是将file.c文件恢复到本地最新的commit记录的状态，也可以认为是撤销对该文件的修改。如果在本地对于文件进行了一些非功能上的修改，比如加入的debug信息，可以通过`git checkout .`将所有的修改都撤销。在`git pull` 之前如果想撤销之前的修改也可以进行`checkout` 操作。

#### 基本操作： status
`git status` 命令是查看当前本地的文件相对于`git log` 中的commit记录的状态。可以看到哪个文件修改了(modefied)，或者删除了(deleted)等。在`git add` 之前可以通过该命令查看具体应该add那个文件。

#### 基本操作： diff
`git diff file.c` 命令是查看当前本地的文件相对于本地的commit做了哪些具体的修改。其中file.c可以通过`git status`命令进行获取。

#### 基本操作：reset
`git reset <commit ID>` 将本地的提交记录回退到之前某一个提交节点上。然后在本地进行修改之后可以通过 `git push -f origin master` 将结果push到远程仓库。


