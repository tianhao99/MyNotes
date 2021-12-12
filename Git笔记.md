# Git的简单使用

## 常用命令

### 仓库

```dockerfile
# 在当前目录新建一个本地Git代码库
$ git init

# 新建一个目录，将其初始化为Git代码库
$ git init [project-name]

# 下载一个项目和它的整个代码历史
$ git clone [url]
```



### 配置

```dockerfile
# 显示当前的Git配置
$ git config --list

# 编辑Git配置文件
$ git config -e [--global]

# 设置提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```

### 增加/删除文件

```dockerfile
# 添加指定文件到暂存区
$ git add [file1] [file2] ...

# 添加指定目录到暂存区，包括子目录
$ git add [dir]

# 添加当前目录的所有文件到暂存区
$ git add .

# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
$ git add -p

# 删除工作区文件，并且将这次删除放入暂存区
$ git rm [file1] [file2] ...

# 停止追踪指定文件，但该文件会保留在工作区
$ git rm --cached [file]

# 改名文件，并且将这个改名放入暂存区
$ git mv [file-original] [file-renamed]
```



### 代码提交

```dockerfile
# 提交暂存区到仓库区
$ git commit -m [message]

# 提交暂存区的指定文件到仓库区
$ git commit [file1] [file2] ... -m [message]

# 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -a

# 提交时显示所有diff信息
$ git commit -v

# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message]

# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...
```



### 分支

```dockerfile
# 列出所有本地分支
$ git branch

# 列出所有远程分支
$ git branch -r

# 列出所有本地分支和远程分支
$ git branch -a

# 新建一个分支，但依然停留在当前分支
$ git branch [branch-name]

# 新建一个分支，并切换到该分支
$ git checkout -b [branch]

# 新建一个分支，指向指定commit
$ git branch [branch] [commit]

# 新建一个分支，与指定的远程分支建立追踪关系
$ git branch --track [branch] [remote-branch]

# 切换到指定分支，并更新工作区
$ git checkout [branch-name]

# 切换到上一个分支
$ git checkout -

# 建立追踪关系，在现有分支与指定的远程分支之间
$ git branch --set-upstream [branch] [remote-branch]

# 合并指定分支到当前分支
$ git merge [branch]

# 选择一个commit，合并进当前分支
$ git cherry-pick [commit]

# 删除分支
$ git branch -d [branch-name]

# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```



### 标签

```dockerfile
# 列出所有tag
$ git tag

# 新建一个tag在当前commit
$ git tag [tag]

# 新建一个tag在指定commit
$ git tag [tag] [commit]

# 删除本地tag
$ git tag -d [tag]

# 删除远程tag
$ git push origin :refs/tags/[tagName]

# 查看tag信息
$ git show [tag]

# 提交指定tag
$ git push [remote] [tag]

# 提交所有tag
$ git push [remote] --tags

# 新建一个分支，指向某个tag
$ git checkout -b [branch] [tag]
```



### 查看信息

```dockerfile
# 显示有变更的文件
$ git status

# 显示当前分支的版本历史
$ git log

# 显示commit历史，以及每次commit发生变更的文件
$ git log --stat

# 搜索提交历史，根据关键词
$ git log -S [keyword]

# 显示某个commit之后的所有变动，每个commit占据一行
$ git log [tag] HEAD --pretty=format:%s

# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
$ git log [tag] HEAD --grep feature

# 显示某个文件的版本历史，包括文件改名
$ git log --follow [file]
$ git whatchanged [file]

# 显示指定文件相关的每一次diff
$ git log -p [file]

# 显示过去5次提交
$ git log -5 --pretty --oneline

# 显示所有提交过的用户，按提交次数排序
$ git shortlog -sn

# 显示指定文件是什么人在什么时间修改过
$ git blame [file]

# 显示暂存区和工作区的差异
$ git diff

# 显示暂存区和上一个commit的差异
$ git diff --cached [file]

# 显示工作区与当前分支最新commit之间的差异
$ git diff HEAD

# 显示两次提交之间的差异
$ git diff [first-branch]...[second-branch]

# 显示今天你写了多少行代码
$ git diff --shortstat "@{0 day ago}"

# 显示某次提交的元数据和内容变化
$ git show [commit]

# 显示某次提交发生变化的文件
$ git show --name-only [commit]

# 显示某次提交时，某个文件的内容
$ git show [commit]:[filename]

# 显示当前分支的最近几次提交
$ git reflog
```



### 远程同步

```dockerfile
# 下载远程仓库的所有变动
$ git fetch [remote]

# 显示所有远程仓库
$ git remote -v

# 显示某个远程仓库的信息
$ git remote show [remote]

# 增加一个新的远程仓库，并命名
$ git remote add [shortname] [url]

# 取回远程仓库的变化，并与本地分支合并
$ git pull [remote] [branch]

# 上传本地指定分支到远程仓库
$ git push [remote] [branch]

# 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --force

# 推送所有分支到远程仓库
$ git push [remote] --all
```



### 撤销

```dockerfile
# 恢复暂存区的指定文件到工作区
$ git checkout [file]

# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]

# 恢复暂存区的所有文件到工作区
$ git checkout .

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]

# 重置暂存区与工作区，与上一次commit保持一致
$ git reset --hard

# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]

# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
$ git revert [commit]

# 暂时将未提交的变化移除，稍后再移入
$ git stash
$ git stash pop
```



### 其他

```dockerfile
# 生成一个可供发布的压缩包
$ git archive
```





## SSH公钥

### **1、获取公钥**

终端输入：

```D
ssh-keygen -t rsa
```

![image-20211211162936646](https://pledge99.oss-cn-beijing.aliyuncs.com/img/%E5%85%AC%E9%92%A5.png)

根据刚才的位置，找到创建的.ssh文件夹

要打开隐藏的文件

- Mac系统：command + shift + .

### **2、打开id_rsa.pub文件**

![image-20211211163918433](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211163918433.png)

复制里面的全部内容

![image-20211211164002493](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211164002493.png)

### 3、到码云-->个人主页-->SSH公钥设置

标题可以改成当前机器名字，如家里、办公室电脑等

![image-20211211164335054](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211164335054.png)



## 新建仓库

![image-20211211165439655](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211165439655.png)

## 克隆仓库

### 1、复制仓库地址

建议用SSH链接，这样后边不用每次push都输入密码；

![image-20211211170258032](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211170258032.png)

### 2、Git命令克隆到本地仓库

在目标文件夹内部，执行克隆命令

![image-20211211170159839](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211170159839.png)

## IDEA中集成Git

### 1、新建项目，绑定Git

- 直接将远程克隆下来的，文件目录copy到项目目录下即可

![image-20211211175135166](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211175135166.png)

- 直接扔到工程目录下

  ![image-20211211175207084](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211175207084.png)

- copy后刷新IDEA，出现Git图标

![image-20211211175111505](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211175111505.png)

### 2、提交方式：

- 直接调用按钮添加或者提交
  - ![image-20211211183900804](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211183900804.png)
- 使用命令行提交
  - git add .
  - git commit -m "这里写说明，添加了啥东西"
  - git push

![image-20211211184030602](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211184030602.png)

### 3、提交后查看

![image-20211211184123350](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211211184123350.png)



## 坑！！！

### 1、执行push命令，每次需要输入密码

- 方法一：【亲测对我无效】、

  - 克隆仓库时，直接克隆SSH地址

  - 已经克隆了，在隐藏文件.git/config中，直接改url，将原本https的链接换成SSH的地址即可

    ![image-20211212011125543](https://pledge99.oss-cn-beijing.aliyuncs.com/img/image-20211212011125543.png)

- 方法二：【在方法一折腾的基础上】

  - 在终端执行

    ```
    ssh-add -L
    ```

  - 再执行

    ```
    ssh-add
    ```

  再退出执行git push就不需要输入密码了
