#### 猴子都能懂的GIT入门-高级篇笔记

时间：2019年6月16日

天气：晴

#### 二、操作分支

##### 1、建立分支

创建分支：使用branch命令来创建分支。

```
git branch <branchname>
```

创建名为issue1的分支。 

```
git branch issue1
```

不指定参数直接执行branch命令的话，可以显示分支列表。 前面有*的就是现在的分支。 

```
git branch
  issue1
* master
```

##### 2、切换分支

切换分支：使用checkout命令。

```
git checkout <branch>
```

```
git checkout issue1
Switched to branch 'issue1'
```

在checkout命令指定 -b选项执行，可以创建分支并进行切换。 

```
git checkout -b <branch>
```

在切换到issue1分支的状态下提交，历史记录会被记录到issue1分支。在myfile.txt添加内容，然后提交。

```
git add myfile.txt
git commit -m "添加add的说明"
[issue1 b2b23c4] 添加add的说明
 1 files changed, 1 insertions(+), 0 deletions(-)
```

目前的历史记录：

![pic23](G:\Github projects\OnlyForLearnGit\picInFile\pic23.PNG)

##### 3、合并分支

向master分支合并issue1分支的修改。

合并分支时，需要执行merge指令：

```
git merge <commit>
```

作用：该命令将指定分支导入到HEAD指定的分支。

先切换master分支，然后把issue1分支导入到master分支。 

```
git checkout master
Switched to branch 'master'
```

![pic24](G:\Github projects\OnlyForLearnGit\picInFile\pic24.PNG)

之后再执行merge命令：

```
$ git merge issue1
Updating 6baed28..3f965c9
Fast-forward
 tutorial/myfile.txt | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 tutorial/myfile.txt
```

master分支指向的提交移动到和issue1同样的位置。这个是fast-forward（快进）合并。 

![pic25](G:\Github projects\OnlyForLearnGit\picInFile\pic25.PNG)

##### 4、删除分支

既然issue1分支的内容已经顺利地合并到master分支了，现在可以将其删除了。 

删除分支：在branch命令指定-d选项执行，以删除分支。 

```
git branch -d <branchname>
```

执行命令：

```
git branch -d issue1
Deleted branch issue1 (was 3f965c9).
```

使用branch命令来查看分支：

```
git branch
* master
```

![pic26](G:\Github projects\OnlyForLearnGit\picInFile\pic26.PNG)

##### 5、并行操作

创建issue2分支和issue3分支，并切换到issue2分支。 （本地）

```
$ git branch issue2
$ git branch issue3
$ git checkout issue2
Switched to branch 'issue2'
$ git branch
* issue2
  issue3
  master
```

![pic27](G:\Github projects\OnlyForLearnGit\picInFile\pic27.PNG)

在issue2分支的myfile.txt添加commit命令的说明后提交。

![pic28](G:\Github projects\OnlyForLearnGit\picInFile\pic28.PNG)

接着切换到issue3分支。

```
git checkout issue3
Switched to branch 'issue3'
```

打开myfile.txt文档。由于在issue2分支添加了commit命令的说明，所以issue3分支的myfile.txt里只有add命令的说明。

添加pull命令的说明后提交。

![pic29](G:\Github projects\OnlyForLearnGit\picInFile\pic29.PNG)

##### 6、解决合并的冲突

把issue2分支和issue3分支的修改合并到master。 

切换master分支后，与issue2分支合并。 

```
$ git checkout master
Switched to branch 'master'
$ git merge issue2
Updating b2b23c4..8f7aa27
Fast-forward
 myfile.txt |    2 ++
 1 files changed, 2 insertions(+), 0 deletions(-)
```

执行fast-forward（快进）合并。 

![pic30](G:\Github projects\OnlyForLearnGit\picInFile\pic30.PNG)

接着合并issue3。

```
$ git merge issue3
Auto-merging myfile.txt
CONFLICT (content): Merge conflict in myfile.txt
Automatic merge failed; fix conflicts and then commit the result.
```

此时产生冲突。因为在同一行进行了修改，所以产生了冲突。这时myfile.txt的内容如下：

```
连猴子都懂的Git命令
add 把变更录入到索引中
<<<<<<< HEAD
line2：issue2的操作
=======
line2：issue3的操作
>>>>>>> issue3
```

 修改冲突：

```
连猴子都懂的Git命令
add 把变更录入到索引中
line2：issue2的操作
line3：issue3的操作
```

重新提交：

```
$ git add myfile.txt
$ git commit -m "合并issue3分支"
# On branch master
nothing to commit (working directory clean)
```

![pic31](G:\Github projects\OnlyForLearnGit\picInFile\pic31.PNG)

##### 7、用rebase合并

合并issue3分支的时候，使用rebase可以使提交的历史记录显得更简洁。 

暂时取消issue3的合并。

```
git reset --hard HEAD~
```

![pic32](G:\Github projects\OnlyForLearnGit\picInFile\pic32.PNG)

切换到issue3分之后，对master执行rebase：

```
$git rebase master
First, rewinding head to replay your work on top of it...
Applying: issue3的操作
Using index info to reconstruct a base tree...
M       tutorial/myfile.txt
Falling back to patching base and 3-way merge...
Auto-merging tutorial/myfile.txt
CONFLICT (content): Merge conflict in tutorial/myfile.txt
error: Failed to merge in the changes.
hint: Use 'git am --show-current-patch' to see the failed patch
Patch failed at 0001 issue3的操作

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort"
```

（跟教程不同，myfile.txt文件出现了乱码：

```
连猴子都懂的Git命令
add 把变更录入到索引中
<<<<<<< HEAD
line2：issue2的操作
=======
line2：issue3的操作
>>>>>>> issue3鐨勬搷浣?
```

和merge时的操作相同，修改在myfile.txt发生冲突的部分。 

rebase的时候，修改冲突后的提交不是使用commit命令，而是执行rebase命令指定 --continue选项。若要取消rebase，指定 --abort选项。

```
$ git add .
$ git rebase --continue
Applying: issue3的操作
```

![pic33](G:\Github projects\OnlyForLearnGit\picInFile\pic33.PNG)



这样，在master分支的issue3分支就可以fast-forward合并了。切换到master分支后执行合并。 

```
$ git checkout master
Switched to branch 'master'
$ git merge issue3
Updating 8f7aa27..96a0ff0
Fast-forward
 myfile.txt |    1 +
 1 files changed, 1 insertions(+), 0 deletions(-)
```

myfile.txt的最终内容和merge是一样的，但是历史记录如下。 

![pic35](G:\Github projects\OnlyForLearnGit\picInFile\pic35.PNG)







