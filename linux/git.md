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
  
如果是多人协作更新一个Repository，或者多台电脑更新就会出现新的问题。



#### 进阶操作：pull
`git pull` 命令是将远程的修改更新到本地，要求本地相对于远程有修改（如果有，则需要进行merge操作）。
