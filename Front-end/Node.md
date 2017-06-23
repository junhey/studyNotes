> nodejs、mongodb、git、linux和一些其他常用的命令

nodejs

淘宝npm镜像

npm install -g cnpm --registry=https://registry.npm.taobao.org
全局安装后以后就可以 cnpm install 了，在国内npm不稳定的时候cpm极其管用！
npm 参数

-g 全局
--save 安装后并且把信息存入 package.json中的dependencies
--save-dev 安装后并且把信息存入 package.json中的devDependencies
package

nvm 多版本node管理

node-dev 实时重启node应用
node-dev app.js
mongodb

安装使用

1、下载mongodb到任意目录（以'D:\MongoDB'为例）
2、进入D:\MongoDB目录，新建data和logs文件夹作为数据和日志输出目录
3、命令窗口进入D:\MongoDB\bin目录，启动，命令如下：
mongod --dbpath="D:\MongoDB\data" --logpath="D:\MongoDB\logs\mongodb.log"
4、启动成功后，默认的port一般为27017
注：mongodb每次需要手动输入命令启动，比较麻烦，可以写一个.bat或者.sh来快捷启动mongodb
备份/还原

1、备份，命令如下：
mongodump -h 数据库地址 -d 数据库名 -o 输出路径
2、还原，命令如下：
mongorestore -h 数据库地址 -d 数据库名 输入路径
3、eg. 数据库地址 localhost:27017 数据库名 blog 输出路径 "D:\MongoDB\export" 输入路径 "D:\MongoDB\import"
工具

一个GUI管理工具，Robomongo，类似于mysql的phpmyadmin。
git

常用命令

配置
git config --global user.name "hbmu"
git config --global user.email "mhbseal@163.com"
git config --global color.ui true
git config --global alias.co checkout 命令行代理
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.br branch
git config -l 配置详情

提交纪录
git log 查看所有提交纪录
git log <file> 该文件的提交纪录
git log --online 每条记录单行显示
git log --graph 分支合并图
git reflog 查看历史提交纪录（从本地仓库创建之后的所有纪录，包括本地删除过的commit）

文件操作
git checkout -- <file> 撤销工作区某个文件的修改
git checkout . 撤销工作区的修改
git add <file> 提交工作区的某个文件到暂存区（新增和修改）
git add . 提交工作区的所有文件（新增、修改）到暂存区
git add -u 提交工作区的所有文件（修改、删除）到暂存区
git add -A 提交工作区的所有文件（新增、修改、删除）到暂存区
git rm <file> 从工作区中删除某文件
git rm <file> --cached 从工作区中删除某文件，但不删除文件实体
git commit <file> 提交暂存区的某个文件到本地分支
git commit 提交暂存区的所有文件到本地分支
git commit -m 'comment' 同上，加注释
git commit . 相当于git add -u + git commit
git commit -a 同上
git commit -am 'comment' 同上，加注释
git commit --amend 修改commit的注释(vim)
git commit --amend -m 'updatecomment' 修改commit的注释(直接)
git reset -- <file> 撤销出暂存区某个文件的add
git reset  撤销出暂存区的add
git reset --hard HEAD^ 撤销最后一次commit
git reset --hard <$id> 恢复到某次commit的状态

查看diff
git diff <file> 查看（某个文件）工作区和本地分支的diff
git diff --staged <file> 查看（某个文件）暂存区和本地分支的diff
git diff --cached <file> 同上
git diff <$id> <$id> 查看两次commit之间的diff

分支管理
git branch 查看本地分支
git branch -r 查看远程分支
git branch -v 查看本地各个分支最后提交信息
git branch -a 查看所有分支
git branch --merged 查看已经被合并到当前分支的分支
git branch --no-merged 查看尚未被合并到当前分支的分支
git branch <branchname> 基于当前分支来新建分支
git checkout -b <branchname> 同上，并且切换到新分支
git branch <branchname> <start-point> 基于另一个起点（分支名称，提交名称或标签名称）来新建的分支
git checkout -b <branchname> <start-point> 同上，并且切换到新分支
git branch -f <branchname> <start-point> 同上上，强制
git branch -d <branchname> 删除某个分支
git branch -D <branchname> 强制同上的操作（未被合并的分支不提示合并直接删除）
git branch -m <oldbranch> <newbranch> 移动或重命名分支
git branch -M <oldbranch> <newbranch> 强制同上的操作
git branch --set-upstream-to <origin>/<remotebranch> <localbranch> 关联originbranch和localbranch

分支合并
git merge <branch> 将分支合并到当前分支
git merge --no-ff <branch> 将分支合并到当前分支，非Fast-Foward方式
git merge <origin> <remotebranch>  将远程分支合并到当前分支

缓存工作区的修改（不指定<stash>的情况下默认为最新的）
git stash 保存当前到缓存
git stash list 列出所有缓存
git stash apply <stash> 恢复缓存的内容
git stash pop <stash> 恢复缓存的内容，并删除缓存
git stash drop <stash> 删除缓存
git stash clear 删除所有缓存

远程分支
git pull 拉取远程仓库所有分支，并且auto merged
git pull --no-ff 拉取远程仓库所有分支并且auto merged，非Fast-Foward方式
git pull <origin> <remotebranch> 拉取远程仓库某个分支到本地
git pull <origin> <remotebranch>:<localbranch> 同上，自定义本地分支名称
git fetch 拉取远程仓库所有分支，fetch和pull的区别就是不auto merged
git push 推送当前分支到与远程matching的分支
git push <origin> <localbranch> 将本地分支推送到与远程matching的分支，远程没有则创建与本地同名分支
git push -u <origin> <localbranch> 同上，并且建立关联
git push <origin> <localbranch>:<remotebranch> 同上，自定义远程分支名称
git push <origin> :<remotebranch> 删除远程分支

远程仓库
git clone <url> <dir> 克隆仓库到本地 dir（可选）
git remote 查看远程仓库名称
git remote -v 查看远程仓库名称、地址、权限
git remote show <name> 查看远程仓库状态
git remote add <name> <url> 添加远程仓库
git remote set-url <name> <newurl> 修改远程仓库地址
git remote rm <name> 删除远程仓库
linux

常用命令

tar -zcvf 压缩后的文件(后缀名.tar.gz,.tar等) 被压缩文件 压缩
tar -zxvf 被解压文件(后缀名.tar.gz,.tar等) 解压

ln -s sourcefile targetfile 软连接，类似win下快捷方式
other

ssh/scp

ssh user@host ssh远程
scp localpath user@host:remotepath 上传
scp user@host:remotepath localpath 下载