#### 猴子都能懂的Git入门-高级篇

2019年6月17日

天气：晴

##### 四、标签

##### 1、标签（tag）介绍

定义：标签是为了**更方便地参考提交**而给它标上易懂的名称。 

种类：Git可以使用2种标签——轻标签和注解标签。打上的标签是固定的，**不能像分支那样可以移动位置**。 

**轻标签**

- 添加名称

**注解标签**

- 添加名称
- 添加注解
- 添加签名

一般情况下，发布标签是采用注解标签来添加注解或签名的。**轻标签**是为了在**本地暂时使用**或**一次性使用**。 

![pic40](G:\Github projects\OnlyForLearnGit\picInFile\pic40.PNG)

##### 2、添加轻标签

tag命令：使用tag命令来添加标签，在<tagname>执行标签的名称。

```
git tag <tagname>
```

在HEAD指向的提交里添加名为apple的标签，请执行以下的命令。 

```
git tag apple
```

没有参数执行tag，可以显示标签列表：

```
$ git tag
apple
```

在log命令添加 --decorate选项执行，可以显示包含标签的历史记录。

```
$ git log --decorate
commit e7978c94d2104e3e0e6e4a5b4a8467b1d2a2ba19 (HEAD, tag: apple, master)
Author: yourname <yourname@yourmail.com>
Date:   Wed Jul 18 16:43:27 2012 +0900

    first commit
```

##### 3、添加注解标签

方法：若要添加注解标签，可以在tag命令指定 -a选项执行。执行后会启动编辑区，请输入注解，也可以指定-m选项来添加注解。 

```
git tag -a <tagname>
```

举例：在HEAD指向的提交里添加名为banana的标签，可以执行以下命令：

```
git tag -am "连猴子都懂的Git" banana
```

如果在tag命令指定-n选项执行，可以显示标签的列表和注解。 

```
$ git tag -n
apple           first commit
banana          连猴子都懂的Git
```

标签的状态：

![pic41](G:\Github projects\OnlyForLearnGit\picInFile\pic41.PNG)



##### 4、删除标签

方法：若要删除标签，在tag命令指定 -d选项执行。

```
$ git tag -d <tagname>
```

