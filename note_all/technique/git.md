# Git 的相关操作笔记

## 如何在git上将多次commit合并为一个
在开发新功能或者debug的时候，多个步骤往往伴随着多次commit，如果直接push到远端main分支上，会产生比较乱的commit信息。
这个时候需要从main分支上拉出去一个新的分支，tmp分支。并且与远端main同步。
```
# 创建tmp分支
git branch tmp

# 同步远程main分支 
git pull origin main
```
然后在tmp分支下进行开发，期间可以有多次commit。  
开发完成后，并且测试代码没问题后，切换到main分支，并且使用merge命令，如下：
```
git checkout main
git merge --squash tmp
```
这就将tmp分支中所有的修改都同步了过来，这个时候只是代码进行了合并，没有进行commit。
然后使用如下命令，将代码commit到本地和push到远端：
```
git commit -m "message"
git push -u origin main
```
完成对main分支的操作后，删除tmp分支
```
git branch -D tmp
```

参考资料：  
* [git 合并多次提交为一次提交](https://www.jianshu.com/p/68a55caa4501)
