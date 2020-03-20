git  进入文件夹分割符是'/'
cd C:/....


设置Git的user name和email：
git config --global user.name "string"
git config --global user.email "string"

查看配置列表
git config --lis

生成SSH密钥过程
查看是否已经有了ssh密钥：cd ~/.ssh
ssh-keygen -t rsa -C "${email}"

前言：
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
	
正文
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

测试分支合并
