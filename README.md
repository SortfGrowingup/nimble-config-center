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

创建本地仓库 	———— git init 
添加单个文件流程：
1.添加到暂存区				———— git add [文件名]
2.把文件提交到仓库			———— git commit -m "注释内容"
3.查看是否有文件没有提交	———— git status
On branch master
nothing to commit, working tree clean

创建文件夹 		———— mkdir [文件夹名]
删除文件夹		———— git rm -rf [文件夹名]
编辑文件夹名	———— git mv -f [旧文件夹名] [新文件夹名]

创建文件 		———— touch [文件名+后缀]
删除文件 		———— rm [文件名]
编辑文件名 		———— git mv [旧文件名] [新文件名]
编辑文件内容	———— vim [文件名]
查看文件内容	———— cat [文件名]