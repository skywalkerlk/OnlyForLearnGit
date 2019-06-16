#### 猴子都能懂的GIT入门-高级篇笔记

时间：2019年6月16日

天气：晴

##### 一、分支介绍

##### 1、什么是分支

背景：在开发软件时，可能有多人同时为同一个软件开发功能或修复BUG，可能存在多个Release版本，并且需要对各个版本进行维护。

Git的优势：Git的分支功能可以支持同时进行多个功能的开发和版本管理。 

分支：分支是为了将修改记录的整体流程**分叉保存**。 分叉后的分支不受其他分支的影响，所以在同一个数据库里可以同时进行多个修改。

分支操作：分叉的分支可以合并。  

实际使用：为了不受其他开发人员的影响，您可以在主分支上建立自己专用的分支。完成工作后，将自己分支上的修改合并到主分支。因为每一次提交的历史记录都会被保存，所以当发生问题时，定位和修改造成问题的提交就容易多了。 

![pic12](G:\Github projects\OnlyForLearnGit\picInFile\pic12.PNG)

```
tips：要发挥分支的最大威力，不同人员的开发工作最好进行比较好的解耦。不然就是要花大量时间解决冲突了。
```

master分支：在数据库进行最初的提交后, Git会创建一个名为master的分支。因此之后的提交，在**切换分支之前**都会添加到master分支里。

##### 2、分支的运用

 在Git您可以自由地建立分支。但是，要先确定运用规则才可以有效地利用分支。这里我们会介绍两种分支 (“Merge分支”和 “Topic分支” ) 的运用规则。

**Merge分支**

用途：Merge分支是为了可以随时发布release而创建的分支，它还能作为Topic分支的源分支使用。保持分支稳定的状态是很重要的。如果要进行更改，通常先创建Topic分支，而针对该分支，可以使用Jenkins之类的CI工具进行自动化编译以及测试。

通常，大家会将master分支当作Merge分支使用。

**Topic分支**

Topic分支是为了开发新功能或修复Bug等任务而建立的分支。若要同时进行多个的任务，请创建多个的Topic分支。

Topic分支是从稳定的Merge分支创建的。完成作业后，要把Topic分支合并回Merge分支。

##### 3、分支的切换

checkout操作：若要切换作业的分支，就要进行checkout操作。进行checkout时，git会从工作树还原向目标分支提交的修改内容。checkout之后的提交记录将被追加到目标分支。 

**HEAD**

作用：HEAD指向的是现在使用中的分支的最后一次更新。 通常默认指向master分支的最后一次更新。通过移动HEAD，就可以变更使用的分支。 

![pic13](G:\Github projects\OnlyForLearnGit\picInFile\pic13.PNG)

**stash**

场景：**还未提交**的修改内容以及**新添加**的文件，留在索引区域或工作树的情况下切换到其他的分支时，修改内容会从原来的分支移动到目标分支。 

但是如果在checkout的目标分支中**相同的文件也有修改**，checkout会失败的。这时：要么先提交修改内容，要么用stash暂时保存修改内容后再checkout。 

定义：stash是临时保存文件修改内容的区域。stash可以暂时保存工作树和索引里还没提交的修改内容，您可以事后再取出暂存的修改，应用到原先的分支或其他的分支上。 

##### 4、分支的合并

合并分支的2种方法：使用merge或rebase。使用这2种方法，合并后分支的历史记录会有很大的差别。 

**merge**

使用merge可以合并多个历史记录的流程。 如下图所示，bugfix分支是从master分支分叉出来的。 

![pic14](G:\Github projects\OnlyForLearnGit\picInFile\pic14.PNG)

**fast-forward合并**：合并 bugfix分支到master分支时，**如果master分支的状态没有被更改过**，那么这个合并是非常简单的。bugfix分支的历史记录包含master分支所有的历史记录，所以通过把master分支的位置移动到bugfix的最新分支上，Git  就会合并。这样的合并被称为fast-forward（快进）合并。 

![pic15](G:\Github projects\OnlyForLearnGit\picInFile\pic15.PNG)

但是，master分支的历史记录有可能在bugfix分支分叉出去后有新的更新。这种情况下，要把master分支的修改内容和bugfix分支的修改内容**汇合**起来。

![pic16](G:\Github projects\OnlyForLearnGit\picInFile\pic16.PNG)

因此，合并两个修改会生成一个提交。这时，master分支的HEAD会移动到该提交上。 

![pic17](G:\Github projects\OnlyForLearnGit\picInFile\pic17.PNG)

![pic18](G:\Github projects\OnlyForLearnGit\picInFile\pic18.PNG)

**rebase**

跟merge的例子一样，如下图所示，bugfix分支是从master分支分叉出来的。 

![pic19](G:\Github projects\OnlyForLearnGit\picInFile\pic19.PNG)

如果使用rebase方法进行分支合并，会出现下图所显示的历史记录。

![pic20](G:\Github projects\OnlyForLearnGit\picInFile\pic20.PNG)

解释说明：首先，rebase bugfix分支到master分支, bugfix分支的历史记录会添加在master分支的后面。如图所示，历史记录成一条线，相当整洁。

这时移动提交X和Y有可能会发生冲突，所以需要修改各自的提交时发生冲突的部分。

![pic21](G:\Github projects\OnlyForLearnGit\picInFile\pic21.PNG)

rebase之后，master的HEAD位置不变。因此，要合并master分支和bugfix分支，即是将master的HEAD移动到bugfix的HEAD这里。 

![pic22](G:\Github projects\OnlyForLearnGit\picInFile\pic22.PNG)

```
merge和rebase小结：
Merge和rebase都是合并历史记录，但是各自的特征不同。
merge：保持修改内容的历史记录，但是历史记录会很复杂。
rebase：历史记录简单，是在原有提交的基础上将差异内容反映进去。因此，可能导致原本的提交内容无法正常运行。

可以根据开发团队的需要分别使用merge和rebase。例如，想简化历史记录，在topic分支中更新merge分支的最新代码，请使用rebase。向merge分支导入topic分支的话，先使用rebase，再使用merge。

```

##### 5、topic分支和merge分支运用实例

参见：https://backlog.com/git-tutorial/cn/stepup/stepup1_5.html

https://nvie.com/posts/a-successful-git-branching-model/







