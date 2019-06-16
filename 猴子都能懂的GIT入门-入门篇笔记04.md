### 猴子都能懂的GIT入门-入门篇笔记

时间：2019年6月16日

天气：晴

##### 三、共享数据库

##### 1、push到远程数据库

可以给远程数据库取一个别名。这样，下次推送的时候就不需要输入长串的远程数据库地址了。在这个教程里，远程数据库命名为“origin”。

可以使用remote指令添加远程数据库：

```
git remote add <name> <url>
```

 例子：

```
git remote add origin https://[your_space_id].backlogtool.com/git/[your_project_key]/tutorial.git
```

执行推送或者拉取的时候，如果省略了远程数据库的名称，则默认使用名为”origin“的远程数据库。因此一般都会把远程数据库命名为origin。 

使用push命令向数据库推送更改内容。<repository>处输入目标地址，<refspec>处指定推送的分支。 

```
git push <repository> <refspec>...
```

运行以下命令便可向远程数据库‘origin’进行推送。当执行命令时，如果您指定了-u选项，那么下一次推送时就可以省略分支名称了。但是，首次运行指令向空的远程数据库推送时，必须指定远程数据库名称和分支名称。 

```
git push -u origin master
Username: <用户名>
Password: <密码>
Counting objects: 3, done.
Writing objects: 100% (3/3), 245 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://nulab.backlog.jp/git/BLG/tutorial.git
 * [new branch]      master -> master
```

##### 2、克隆远程数据库

使用clone指令可以复制数据库。在<repository>指定远程数据库的URL，  在<directory>指定新目录的名称。

```
git clone <repository> <directory>
```

一个例子：

```
$ git clone https://nulab.backlog.jp/git/BLG/tutorial.git tutorial2
Cloning into 'tutorial2'...
Username: <用户名>
Password: <密码>
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
```

查看目录，检查是否克隆成功。

##### 3、从克隆数据库中push

修改文件，使用git add和git commit提交，用git push推送变更。

当在克隆的数据库目录执行推送时，您可以省略数据库和分支名称。 

##### 4、从远程数据库pull

使用pull指令进行拉取操作。省略数据库名称的话，会在名为origin的数据库进行pull。 

```
git pull <repository> <refspec>...
```

在Github中对readme.md文件进行修改，然后拉取到本地仓库：

![pic06](G:\Github projects\OnlyForLearnGit\picInFile\pic06.PNG)

同样可以使用log命令来查看历史记录。

##### 5、合并修改记录

场景：在执行pull之后，进行下一次push之前，如果**其他人**进行了推送内容到远程数据库的话，那么你的push将被拒绝。 

原因分析：这种情况下，在读取别人push的变更并进行合并操作之前，你的push都将被拒绝。这是因为，如果不进行合并就试图覆盖已有的变更记录的话，其他人push的变更就会丢失。 

##### 6、解决冲突说明

合并操作：执行合并即可自动合并Git修改的部分。但是，也存在无法自动合并的情况。 

不能合并场景：如果远程数据库和本地数据库的**同一个地方**都发生了修改的情况下，因为无法自动判断要选用哪一个修改，所以就会发生冲突。 

Git会在发生冲突的地方修改文件的内容，如下图。所以我们需要手动修正冲突。 

![pic07](G:\Github projects\OnlyForLearnGit\picInFile\pic07.PNG)

==分割线上方是本地数据库的内容,  下方是远程数据库的编辑内容。 

##### 7、push冲突的状态

一个例子：Github中对readme.md进行修改：

![pic08](G:\Github projects\OnlyForLearnGit\picInFile\pic08.PNG)

本地没有pull，同时对readme.md进行修改并保存：

![pic09](G:\Github projects\OnlyForLearnGit\picInFile\pic09.PNG)

在本地进行push：

![pic10](G:\Github projects\OnlyForLearnGit\picInFile\pic10.PNG)

可以发现发生了错，推送被拒绝（reject）了。

##### 8、解决冲突

解决冲突：为了把变更内容推送到远程数据库，我们必须手动解决冲突。首先运行pull，以从远程数据库取得最新的变更记录。修改文件内容，之后运行git push进行推送。

使用log查看记录。

```
git log --graph --oneline
```

![pic11](G:\Github projects\OnlyForLearnGit\picInFile\pic11.PNG)

