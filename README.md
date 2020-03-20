git  进入文件夹分割符是'/'
cd C:/....

### 前言：

```
1.什么是工作区？
	就是你在电脑上看到的目录，比如目录下testgit里的文件(.git隐藏目录版本库除外)。或者以后需要再新建的目录文件等等都属于工作区范畴。
2.什么是版本库(Repository)？
	作区有一个隐藏目录.git,这个不属于工作区，这是版本库。
	其中版本库里面存了很多东西:
		其中最重要的就是stage(暂存区)
		还有Git为我们自动创建了第一个分支master,以及指向master的一个指针HEAD。
3.提交一个文件会经历什么?
	第一步：把文件添加进去		———— 实际上就是把文件添加到暂存区。
	第二步：提交修改			———— 实际上就是把暂存区的所有内容提交到当前分支上。
4.修改文件和新建文件在git status中有什么区别？
	未到暂存区时：见图片~/git指令图解/{指令}/1.jpg
	在暂存区时：  见图片~/git指令图解/{指令}/2.jpg
5.关于图片提交：
	首先要明确下，所有的版本控制系统，只能跟踪文本文件的改动，比如txt文件，网页，所有程序的代码等；Git也不列外，版本控制系统可以告诉你每次的改 动，但是图片，视频这些二进制文件，虽能也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是知道图片从1kb变成 2kb，但是到底改了啥，版本控制也不知道。
```

### 正文
```
创建本地仓库 					———— git init
(
	会在当前执行命令的根目录下进行创建
)
添加单个文件流程：
1).添加到暂存区					———— git add [文件名]
2).把文件提交到仓库				———— git commit -m "注释内容"
3).查看是否有文件没有提交		———— git status
(
	全部提交的情况下：
	On branch master
	nothing to commit, working tree clean
	红色字体时表示此类文件还没有添加到暂存区
	绿色字体时表示此类文件在暂存区中但还没有提交到仓库
)
4).如果有修改查看文件修改内容	———— git diff [文件名]
```

### 撤销修改和操作：
```
1).知道要删掉那些内容的话，手动更改去掉那些需要的文件，然后add添加到暂存区，最后commit掉。
2).可以按以前的方法直接恢复到上一个版本。使用 git reset  –hard HEAD^
3).把文件在工作区做的修改全部撤销		————git checkout -- [文件名]
(
	1.自动修改后，还没有放到暂存区，使用 撤销修改就回到和版本库一模一样的状态。
	2.另外一种是已经放入暂存区了，接着又作了修改，撤销修改就回到添加暂存区后的状态。
)
```

### 删除文件操作:
```
查看工作日志	———— git log [简化打印内容] -> {--pretty=oneline}
版本回退		———— git reset --hard HEAD~[回退多层版本]{1 ~ ∞} | git reset --hard HEAD^
获取版本号		———— git reflog
(
	例如：
	ef4d850 (HEAD -> master) HEAD@{0}: reset: moving to HEAD~1
	6021d45 HEAD@{1}: commit: 测试
	ef4d850 (HEAD -> master) HEAD@{2}: commit: 丰富指令内容
	e5e12ae HEAD@{3}: commit (initial): 添加README.md文件，里面会包含项目log，git指令集合
)

恢复某一版本	———— git reset --hard [版本号] -> {6021d45}

创建文件夹 		———— mkdir [文件夹名]
删除文件夹		———— git rm -rf [文件夹名]
编辑文件夹名	———— git mv -f [旧文件夹名] [新文件夹名]

创建文件 		———— touch [文件名+后缀]
删除文件 		———— rm [文件名]
编辑文件名 		———— git mv [旧文件名] [新文件名]
编辑文件内容	———— vim [文件名]
查看文件内容	———— cat [文件名]
```

### git远程仓库
```
设置Git的username和email：
git config --global user.name "string"
git config --global user.email "string"

查看配置列表
git config --lis

生成SSH密钥过程
查看是否已经有了ssh密钥：cd ~/.ssh
ssh-keygen -t rsa -C "${user.email}"

先在远程创建仓库，在把本地内容推送到远程上：
1)git remote add origin [远程仓库地址]
2)git push -u origin master
(
	把本地库的内容推送到远程，使用 git push命令，实际上是把当前分支master推送到远程。
	由于远程库是空的，我们第一次推送master分支时，加上了 –u参数，Git不但会把本地的master分支内容推送的远程新的master分支，
	还会把本地的master分支和远程的master分支关联起来， 在以后的推送或者拉取时就可以简化命令。推送成功后，
	可以立刻在github页面中看到远程库的内容已经和本地一模一样了，上面的要输入github的用 户名和密码如下所示：
)
3)git push origin master (之后本地提交远程时使用)


从远程克隆项目到本地：
git clone [远程仓库地址]


创建与合并分支:
	在版本回填退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。
	截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。
	HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支,切换分支级可以I理解为切换时间线。
创建分支		———— git branch [分支名称]
删除分支		———— git branch -d [分支名称]
切换分支 		———— git checkout [分支名称]
查看分支列表	———— git branch
创建并切换分支	———— git checkout -b [分支名称]
分支合并		———— git merge [合并目标分支名称]
(
	git merge命令用于合并指定分支到当前分支上，合并后，再查看readme.txt内容，可以看到，和dev分支最新提交的是完全一样的。
	注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。
)
```