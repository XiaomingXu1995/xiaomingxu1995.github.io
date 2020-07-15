## latex 
有关latex的基本操作笔记。


#### 小操作：
* `\usepackage{ulem} \sout{sentence}` 将`sentence`划掉，效果如同：~~sentence~~ 。

#### 加注释：
* 单行加注释在行首加 `%` 即可。
* 多行加注释运用 `verbatim` 包。
```
\usepackage{verbatim}
\begin{comment}
contents to be in annotation
\end{comment}
```

* 在overleaf中多行加注释，选中需要加注释的部分，`Ctrl + /` 添加注释，再次操作取消多行注释。