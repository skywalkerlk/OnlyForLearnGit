### 猴子都能懂的GIT入门-入门篇笔记

时间：2019年6月16日

天气：晴

#### 一、Git的基础

##### 1、安装Git

Git下载（命令行）：git-scm.com

2、初期设定

设定内容：用户名和邮箱。

用途：作为提交者信息显示在更新历史中。

Git设定保存文件：用户本地目录下的.gitconfig文件中。

如：C:\Users\longkang\\.giconfig

配置方法：用记事本打开输入用户名和邮箱；使用Git命令。

```
git config --global user.name "用户名"
git config --global user.email "邮箱"
```

如果在Windows使用命令行 (Git Bash), 含非ASCII字符的文件名会显示为 "\346\226\260\350\246..."。若设定如下，就可以让含非ASCII字符的文件名正确显示了。 

```
git config --global core.quotepath off
```

如下图所示：

![pic01](G:\Github projects\OnlyForLearnGit\picInFile\pic01.PNG)

若在Windows使用命令行，您只能输入ASCII字符。所以，如果您的提交信息包含非ASCII字符，请不要使用-m选项，而要用外部编辑器输入。外部编辑器必须能与字符编码UTF-8和换行码LF兼容。 

```
git config --global core.editor "\"[使用编辑区的路径]\""
```

##### 2、新建数据库

新建一个文件目录：可以在磁盘的任意一个地方，可以命名为tutorial。

移动到本地Git数据仓库：

```
git init
```

完整命令：

```
mkdir tutorial
cd tutorial
git init
Initialized empty Git repository in /Users/yourname/Desktop/tutorial/.git/
```

##### 3、提交文件

新建一个文件：在tutorial目录下新建一个文本文件，例如sample.txt，输入一些内容。

使用命令确认工作树和索引的状态：

```
git status
```

显示例子：

```
$ git status
# On branch master
#
# Initial commit
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#     sample.txt
nothing added to commit but untracked files present (use "git add" to track)
```

结果分析：‘sample.txt’目前不是历史记录对象。请首先把‘sample.txt’加入到索引，就可以追踪它的变更了。 

将文件加入到索引：

```
git add <file>...
```

```
tips：指定参数「.」，可以把所有的文件加入到索引。

git add .
```

一个例子：

![pic02](G:\Github projects\OnlyForLearnGit\picInFile\pic02.PNG)

将文件加入索引后，可以提交文件。执行commit命令：

```
git commit -m "<对此次提交的说明>"
```

执行commit之后确认状态：

![pic03](G:\Github projects\OnlyForLearnGit\picInFile\pic03.PNG)

可以看到没有新的变更需求需要提交。

使用log命令查看提交记录：

![pic04](G:\Github projects\OnlyForLearnGit\picInFile\pic04.PNG)

```
安装git的同时会安装名为gitk的工具。使用这个工具，可以在GUI下确认提交记录。
gitk
```

