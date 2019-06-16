#### 猴子都能懂的Git入门-高级篇

2019年6月17日

天气：晴

##### 三、远端数据库

##### 1、pull

执行pull可以取得远程数据库的历史记录。 

首先确认更新的本地数据库分支没有任何的更改。 

![pic36](G:\Github projects\OnlyForLearnGit\picInFile\pic36.PNG)

这时只执行fast-forward合并。图中的master是本地数据库的master分支，origin/master是远程数据库的origin的master分支。 

![pic37](G:\Github projects\OnlyForLearnGit\picInFile\pic37.PNG)

如果本地数据库的master分支有新的历史记录，就需要合并双方的修改。 

**执行pull**就可以进行合并。这时，如果没有冲突的修改，就会自动创建合并提交。如果发生冲突的话，要先解决冲突，再手动提交。 

![pic38](G:\Github projects\OnlyForLearnGit\picInFile\pic38.PNG)

##### 2、fetch

场景：执行pull，远程数据库的内容就会自动合并。但是，有时只是想确认本地数据库的内容而不想合并。这种情况下，请使用fetch。 

执行fetch就可以取得远程数据库的最新历史记录。取得的提交会导入到没有名字的分支，这个分支可以从名为FETCH_HEAD的退出。 

例如，在本地数据库和远程数据库的origin，如果在从B进行提交的状态下执行fetch，就会形成如下图所示的历史记录。

![pic39](G:\Github projects\OnlyForLearnGit\picInFile\pic39.PNG) 

在这个状态下，若要把远程数据库的内容合并到本地数据库，可以合并FETCH_HEAD，或者重新执行pull。 

合并后，历史记录会和pull相同。实际上pull的内容是fetch + merge组成的。 

##### 3、push

上面的操作都是本地创建分支，没有push分支。

从本地数据库push到远程数据库时，要fast-forward合并push的分支。如果发生冲突，push会被拒绝的。 

若要共享在本地数据库创建的分支，需要**明确的push**。因此，**没有执行push就不会给远程数据库带来影响，因而可以自由的创建自己的分支**。 

```
注意：基本上，远程数据库共享的提交是不能修改的。如果修改的话，跟远程数据库同步的其他数据库的历史记录会变得很奇怪的。
```

