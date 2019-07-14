### 开始
- 建立仓库
```
git init
```
- 添加文件
```
git add <file>
```
- 提交文件
```
git commit -m <message>
```
- 工作区状态
```
git status
```
- 修改内容
```
git diff
```
### 版本回退
- 历史记录--提交日志
```
git log
git log --pretty=oneline
#可以看到commit id
```
- 回退
```
git reset --hard HEAD^
#HEAD表示当前版本
HEAD^^
HEAD~100
#查看
cat readme.txt
#指定版本
git reset --hard <id>
```
- 记录命令
```
git reflog
```
**工作区**——所在文件夹  
**版本库**——.git文件  
**暂存区**——add的文件
- 查看工作区和版本库里最新版本区别
```
git diff HEAD -- <file>
```
- 撤销修改
```
git checkout -- file
#恢复到最近一次add or commit的状态
git reset HEAD <file>
#暂存区修改回退到工作区
```
- 删除文件
```
git rm <file>
git commit -m ""
```
### 创建SSH
```
ssh-keygen -t rsa -C "youremail@example.com"
#用户主目录下.ssh目录
#包含id_rsa和id_rsa.pub两个文件
#私钥/公钥
```
### 远程仓库
- 关联
```
git remote add origin git@github.com:用户名/仓库名
```
- 推送
```
#第一次推送
git push -u origin master
#将当前分支master推送到远程
#-u 关联本地和远程的master分支
git push origin master
```
- 克隆
```
git clone git@github.com:用户名/仓库名
```
### 分支
- 创建分支
```
#创建并切换 -b
git checkout -b <name>
#等价
git branch <name>
git checkout <name>
```
- 查看分支
```
git branch
```
- 切换分支
```
git checkout <name>
```
- 合并分支
```
git merge <name>
#合并到当前分支
```
Fast-forward 快进模式——删除分支会丢掉分支信息
```
git merge --no-ff -m "merge with no-ff" dev
#--no-ff参数:禁用Fast forward
#强制禁用ff模式Git会在merge时生成一个新的commit(-m)

git log (--graph --pretty=oneline --abbrev-commit)
#查看分支历史
```
- 删除分支
```
git branch -d <name>
#删除未合并分支
git branch -D <name>
```
- 分支合并图
```
git log --graph
```
- 暂存分支
修复bug切换分支，暂存当前分支未提交的工作
```
git stash
#查看
git stash list
#恢复并删除
git stash pop
```
- 查看远程库信息
```
git remote
#详细
git remote -v
```
### 多人协作
```
#第三方
git clone git@github.com:michaelliao/learngit.git
git checkout -b dev origin/dev
......
git push origin dev

#自己推送
......
git push origin dev
#推送失败
#把最新的提交从origin/dev抓下来，然后在本地合并解决冲突再推送
git pull
#若抓取失败，指定本地dev分支与远程origin/dev分支的链接
git branch --set-upstream-to=origin/dev dev
#处理冲突
```
### 标签
- 新标签
```
git tag <name>
#默认标签是打在最新提交的commit上的
#对历史commit打标签
git tag <name> <commit id>
#带说明信息
git tag -a <tagname> -m "Notes."
```
- 查看所有标签
```
git tag
```
- 查看标签信息
```
git show <tagname>
#可以看到说明信息
```
- 操作标签
```
#推送一个本地标签
git push origin <tagname>
#推送全部未推送过的本地标签
git push origin --tags

#删除一个本地标签
git tag -d <tagname>
#删除一个远程标签
git push origin :refs/tags/<tagname>
