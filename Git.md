# 1、Git概述

## 1.5 Git工作机制

1. 工作区：写代码。git add 推送到暂存区，git commit 推送到本地库， git push 推送到远程库（代码托管中心，如GitHub）
2. 工作区-暂存区-本地库-远程库

## 1.6 Git和代码托管中心

代码托管中心是基于网络服务器的远程代码仓库，一般我们简单称为**远程库**

- 局域网
  - GitLab
- 互联网
  - Github
  - Gitee

# 2、Git安装

![image-20231226201037890](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231226201037890.png)

![image-20231226201134218](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231226201134218.png)

![image-20231226201326781](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231226201326781.png)

![image-20231226201449772](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231226201449772.png)

# 3、Git常用命令

| 命令名称                             | 作用               |
| ------------------------------------ | ------------------ |
| git config --global user.name 用户名 | 设置用户签名       |
| git config --global user.email 邮箱  | 设置用户签名       |
| **git init**                         | **初始化本地库**   |
| **git status**                       | **查看本地库状态** |
| **git add 文件名**                   | **添加到暂存区**   |
| **git commit -m “日志信息" 文件名**  | **提交到本地库**   |
| **git reflog**                       | **查看历史记录**   |
| **git reset --hard 版本号**          | **版本穿梭**       |

## 3.1 设置用户签名

### 1）基本语法

| 命令名称                             | 作用         |
| ------------------------------------ | ------------ |
| git config --global user.name 用户名 | 设置用户签名 |
| git config --global user.email 邮箱  | 设置用户签名 |

![image-20231228095339845](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231228095339845.png)

### 2）注意事项		

​		签名的作用就是为了区分不用操作者身份。**Git首次安装必须设置一下用户签名，否则无法提交代码**。设置完成后，在C盘用户目录（`C:\Users\a1072`）下会有`.gitconfig`文件，内容如下：

```json
[user]
	name = ZewardWang
	email = ccor4ng3@gmail.com
```

​		**注意：用户签名和将来登录GitHub的账号没有任何关系**

## 3.2 初始化本地库

### 1）基本语法

​		init就是让Git获取这个目录的管理权。

| 命令名称     | 作用             |
| ------------ | ---------------- |
| **git init** | **初始化本地库** |

### 2）案例实操

```shell
a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo
$ git init
Initialized empty Git repository in E:/CodeProject/gitdemo/.git/

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ ll -a
total 4
drwxr-xr-x 1 a1072 197609 0 Dec 28 10:01 ./
drwxr-xr-x 1 a1072 197609 0 Dec 28 10:00 ../
drwxr-xr-x 1 a1072 197609 0 Dec 28 10:01 .git/

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$
```

## 3.3 查看本地库状态

| 命令名称       | 作用           |
| -------------- | -------------- |
| **git status** | **查看本地库** |

### 3.3.1 首次查看（工作区没有任何文件）

```shell
a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ git status
On branch master #当前处在master分支
No commits yet #当前还没有提交过任何东西
nothing to commit (create/copy files and use "git add" to track) #没有东西需要提交

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$
```

### 3.3.2 新增文件（hello.txt）

```shell
# 在当前目录下添加新文件
a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ vim hello.txt

# 查看当前目录下的文件
a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ ll
total 1
-rw-r--r-- 1 a1072 197609 25 Dec 28 10:05 hello.txt

# 输出文件内容
a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ cat hello.txt
hello git
hello at guigu

# 新增文件后查看状态
a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ git status
On branch master # 当前处在master分支

No commits yet # 没有提交的记录

Untracked files: # 未追踪的文件
  (use "git add <file>..." to include in what will be committed)
        hello.txt

nothing added to commit but untracked files present (use "git add" to track) # 还没有添加需要commit的文件，但是已经追踪到了

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$
```

### 3.3.3 再次查看（检测到未追踪的文件）

## 3.4 添加和删除暂存区

### 3.4.1 将工作区的文件添加到暂存区

| 命令                   | 作用                   |
| ---------------------- | ---------------------- |
| git add 文件名         | 将文件添加到暂存区     |
| git rm --cached 文件名 | 删除添加到暂存区的文件 |

### 3.4.2 查看状态（检测到暂存区有新文件）

```shell
a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ git add hello.txt
warning: in the working copy of 'hello.txt', LF will be replaced by CRLF the next time Git touches it # LF自动转换（换行符）

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ git status
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   hello.txt #绿色，新文件

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ git rm --cached hello.txt # 删除暂存区的文件
rm 'hello.txt'

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ git status
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.txt
nothing added to commit but untracked files present (use "git add" to track)

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$
```

## 3.5 提交本地库

### 3.5.1 将暂存区的文件提交到本地库

| 命令                            | 作用                       |
| ------------------------------- | -------------------------- |
| git commit -m "日志信息" 文件名 | 将暂存区的文件提交到本地库 |

### 3.5.2 查看状态（没有文件需要提交）

```shell
a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ git commit -m "first commit" hello.txt
warning: in the working copy of 'hello.txt', LF will be replaced by CRLF the next time Git touches it
[master (root-commit) 858bb27] first commit
 1 file changed, 2 insertions(+)
 create mode 100644 hello.txt

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ git status
On branch master
nothing to commit, working tree clean # 工作树是干净的，没有东西需要提交

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ git reflog # 查看简易日志
858bb27 (HEAD -> master) HEAD@{0}: commit (initial): first commit

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$ git log # 查看详细日志
commit 858bb27f2cf2bff53b5cc29b05b2fd5525897ca3 (HEAD -> master)
Author: ZewardWang <ccor4ng3@gmail.com>
Date:   Thu Dec 28 10:17:48 2023 +0800

    first commit

a1072@DESKTOP-TOMH1VK MINGW64 /e/CodeProject/gitdemo (master)
$
```

## 3.6 修改文件（hello.txt）

### 3.6.1 查看状态（工作区检测到有文件被修改）

<img src="https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231228102240845.png" alt="image-20231228102240845" style="zoom:150%;" />

### 3.6.2 将修改的文件再次添加暂存区

<img src="https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231228102317726.png" alt="image-20231228102317726" style="zoom:150%;" />

### 3.6.3 查看状态（工作区的修改添加到了暂存区)

<img src="https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231228102424168.png" alt="image-20231228102424168" style="zoom:150%;" />

## 3.7 历史版本

### 3.7.1 查看历史版本

git reflog  查看版本信息

git log 	查看版本详细信息

### 3.7.2 版本穿梭

git reset --hard 版本号

# 4、Git分支操作

## 4.1 什么是分支

## 4.2 分支的好处

## 4.3 分支的操作

| 命令名称            | 作用                       |
| ------------------- | -------------------------- |
| git branch 分支名   | 创建分支                   |
| git branch -v       | 查看分支                   |
| git checkout 分支名 | 切换分支                   |
| git merge 分支名    | 把指定分支合并到当前分支上 |

# 5、GIt团队协作机制

# 6、Github操作

## 6.1 创建远程仓库

![image-20231229104105944](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231229104105944.png)

![image-20231229104324807](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231229104324807.png)

## 6.2 远程仓库操作

| 命令名称                                 | 作用                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| git remote -v                            | 查看当前所有远程地址别名                                     |
| git remote add 别名 远程地址             | 起别名                                                       |
| **git push 别名 分支**                   | **推送本地分支上的内容到远程仓库**                           |
| **git clone 远程地址**                   | **将远程仓库的内容克隆到本地**                               |
| **git pull 远程仓库地址别名 远程分支名** | **将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并** |

### 6.2.1 创建远程仓库别名

#### 1）基本语法

**git remote -v 查看当前所有远程地址别名**

**git remote add 别名 远程地址**

#### 2）案例实操

![image-20231229104935367](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231229104935367.png)

<img src="https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231229104901788.png" alt="image-20231229104901788" style="zoom:150%;" />

### 6.2.2 推送本地分支到远程仓库

#### 1）基本语法

**git push 别名 分支**	（推送的时候可以不用别名，直接使用网址，但是推送的最小单位是分支，必须指定要推送的分支）

#### 2）案例实操

<img src="https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231229105410551.png" alt="image-20231229105410551" style="zoom: 150%;" />

​		推送后可以在远程库上发现代码，注意第一次推送需要登陆github账号

![image-20231229105435079](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231229105435079.png)

### 6.2.3 克隆远程仓库到本地

#### 1）基本语法

git clone 链接

#### 2）案例实操

​		点击此处查看该库的链接

![image-20231229110254243](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231229110254243.png)

<img src="https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231229110734888.png" alt="image-20231229110734888" style="zoom:150%;" />

​		注意克隆public仓库不需要登陆账号

​		克隆会做三件事：1.拉取代码 2.初始化本地仓库 3.创建别名

### 6.2.4 团队内协作

#### 1）基本操作

登录创建仓库的账号，点击仓库的settings

![image-20240101194725241](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101194725241.png)

在打开的页面中点击Collaborators中的manage access中的add people

![image-20240101194834878](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101194834878.png)

在弹出的页面中添加用户

![image-20240101194851998](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101194851998.png)

添加后复制此处的邀请函地址  实例为：https://github.com/ZewardWang/gitdemo/invitations

![image-20240101195010564](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101195010564.png)

加入协作后，该用户就可以更新远程库中的内容；更新后，原用户可以使用  `git pull 别名`   拉取库

### 6.2.5 拉取远程库内容

#### 1）基本语法

**git pull 别名 分支**

#### 2）案例实操

<img src="https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20231229110831606.png" alt="image-20231229110831606" style="zoom:150%;" />

​		拉取后会自动将更新提交到本地库

## 6.3 跨团队协作

​		GitHub中可以通过`用户名/仓库名`的方式精准搜索仓库

​		团队外的协同开发要点击右上角的fork复制到本地

![image-20240101195735534](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101195735534.png)

![image-20240101200022743](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101200022743.png)

​		fork完成之后，可以在当前用户看到一个来自对方的目录，之后就可以在线编辑、pull到本地库进行修改。![image-20240101200101059](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101200101059.png)

​		团队外的人员修改完成后点击Pull requests向原仓库管理提交修改申请

![image-20240101200312777](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101200312777.png)

![image-20240101200347677](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101200347677.png)

![image-20240101200406169](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101200406169.png)

![image-20240101200429237](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101200429237.png)

​		提交后切换回原账号，可以看到pull request

![image-20240101200526285](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101200526285.png)

![image-20240101200547979](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101200547979.png)

​		点开后可以查看详情，还可以添加评论

![image-20240101200700503](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101200700503.png)

​		如果要采纳这个代码，点击merge pull request

## 6.4 SSH免密登录

​		在当前用户目录下启动git bash

```shell
ssh-keygen.exe -t rsa -C 描述
```

​		输入指令后连续三次回车，会在本地生成`id_rsa、id_rsa.pub`两个文件，将id_rsa.pub内容复制到用户的settings-SSH and GPG keys中

![image-20240101201846198](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101201846198.png)

​		添加完成后，就可以使用SSH链接进行pull push等操作（即将上述https链接改成ssh即可）

![image-20240101201922822](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101201922822.png)

# 7、IDEA集成Git

## 7.1 配置Git忽略文件

​		使用IDEA开发中，会有xml、target等文件，这些文件不能上传到远程库，我们只要pom文件和代码

1）创建忽略规则文件`xxxx.ignore`（前缀名随便起，建议是git.ignore）；这个文件的存放位置原则上在哪里都可以，为了便于让~/.gitconfig文件引用，建议也放在用户家目录下。git.ignore文件模板内容如下：

```
# Compiled class file
*.class

# Log file
*.log

# BlueJ files
*.ctxt

# Mobile Tools for Java (J2ME)
.mtj.tmp/

# Package Files #
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar

hs_err_pid*

.classpath
.project
.settings
target
.idea
*.iml
```

2）在.gitconfig文件中引用忽略配置文件（此文件在Windows的家目录中）

```
[user]
	name = ZewardWang
	email = ccor4ng3@gmail.com
[core]
    excludesfile = C:/Users/a1072/git.ignore
注意：这里要使用“正斜线（/）”，不要使用“反斜线（\）“
```

## 7.2 定位Git程序

![image-20240101205430935](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101205430935.png)

## 7.3 初始化本地库

![image-20240101205731749](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101205731749.png)

![image-20240101205801823](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101205801823.png)

​		创建完成后，文件红色代表未追踪；绿色代表添加到暂存区，未提交到本地库；

## 7.4 添加到暂存区

**方法一：右键文件-git-add**

![image-20240101205856389](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101205856518.png)

​		在创建了git之后，每次新建文件会出现如下提示，是否自动追踪：

![image-20240101210121445](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101210121445.png)

**方法二：右键项目根目录，将整个项目进行add**

![image-20240101210248661](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101210248661.png)

## 7.5 提交到本地库

**右键目录-git-commit**

![image-20240101210844624](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101210844624.png)

​		提交后文件变成黑色（表示不需要被提交），已经add一次的文件在修改后会变成蓝色，可以直接commit，不必再add

## 7.6 切换版本

左下角有version control-log

![image-20240101211226978](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101211226978.png)

​		绿色指针表示master指针，黄色表示当前指针，右键版本-checkout revision 版本号即可切换

![image-20240101211336247](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101211336247.png)

​		切换后指针：

![image-20240101211353140](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240101211353140.png)

## 7.7 创建分支

方法一：选择git，再repository里面，点击branches按钮

![image-20240102121516897](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102121516897.png)

方法二：点击IDEA右下角

![image-20240102121545896](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102121545896.png)

## 7.8 切换分支

![image-20240102121722809](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102121722809.png)

## 7.9 合并分支

在当前分支点击右下角分支信息，点击merge into current

![image-20240102122136972](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102122136972.png)

## 7.10 解决冲突问题

![image-20240102122505259](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102122505259.png)

点击merge后会弹出代码对比，通过点击按钮可以手动选择代码，点击apply合并

![image-20240102122555161](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102122555161.png)

# 8、IDEA集成Github

## 8.1 设置Github账号

在setting中点击version control——GitHub（如果没有，到plugins中下载GitHub插件）

![image-20240102123007830](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102123007830.png)

![image-20240102122929144](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102122929144.png)

​		登录方式分为账号登录和口令登录，口令可以从网页GitHub——settings——developer settings——personal access tokens——tokens中生成，生成的时候把权限拉满，口令只能显示一次，刷新就没了，及时复制

## 8.2 分享工程到GitHub

​		通过IDEA可以直接在GitHub中创建远程库并将项目分享到远程库

![image-20240102124555297](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102124555297.png)

![image-20240102124637561](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102124637561.png)

可能由于网络问题，仓库已经创建，但文件未上传，可直接点击上方的push上传

![image-20240102124913384](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102124913384.png)

## 8.3 push推送本地库到远程库

**方法一：工具栏直接push（见上面）**

**方法二：菜单——git——push**

![image-20240102125101034](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102125101034.png)

**方法三：右键项目目录——git——push**

![image-20240102125132387](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102125132387.png)



使用SSH进行push操作：

​		push时在出现的页面点击库名，点击define remote

![image-20240102125350390](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102125350390.png)

​		起一个别名，复制该仓库的ssh链接

![image-20240102125427462](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102125427462.png)

![image-20240102125510678](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102125510678.png)

​		注意：push是将本地库的代码推送到远程库，如果本地库的代码和远程库的代码版本不一致，push 的操作是会被拒绝的。也就是说想要push成功，一定要保证本地库的版本要比远程库的版本高。因此一个成熟的程序员在动手改本地代码之前，一定会先检查一下远程库跟本地库代码的区别，如果本地的代码版本已经落后，切记要先pull拉取一下远程库的代码，将本地的代码更新到最新以后，再提交修改。

## 8.4 pull拉取远程库到本地库

​		注意：pull是拉取远端仓库代码到本地，如果远程库代码和本地库代码不一致，会自动合并，如果自动合并失败，还会涉及到手动解决冲突的问题

**菜单栏git——pull**

![image-20240102130234865](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102130234865.png)

## 8.5 clone克隆远程库到本地

​		我们本地目前没有任何东西，可以直接打开IDEA，从git上克隆项目到本地

![image-20240102130826731](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102130826731.png)

# 9、国内代码托管中心-码云

## 9.1 码云账号注册和登录

## 9.2 码云创建远程库

![image-20240102131522899](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102131522899.png)

## 9.3 IDEA集成码云

### 9.3.1 IDEA安装码云插件

![image-20240102131723252](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102131723252.png)

### 9.3.2 IDEA连接码云

​		在IDEA登录码云账号

![image-20240102131819067](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102131819067.png)

## 9.3.3 IDEA操作码云

**方法一：在没有gittee仓库的情况下直接将项目分享到gitee，会自动创建仓库**

![image-20240102131944940](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102131944940.png)

**方法二：获取https的链接后push代码**

​		方法同上，点击push之后，点击origin，添加一个gitee的链接

![image-20240102132244186](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102132244186.png)

![image-20240102132255691](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102132255691.png)

其他pull等操作参照GitHub，在提交的时候换一下库即可

![image-20240102132453876](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102132453876.png)

## 9.4 导入Github项目

![image-20240102132618085](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102132618085.png)

![image-20240102132629501](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240102132629501.png)

创建仓库完成后，可以点击仓库后面的圈圈同步GitHub的更新



# 10、自建代码托管平台GitLab

## 10.1 Git Lab简介

## 10.2 Git Lab官网地址

官网地址：https://about.gitlab.com/

安装地址：https://gitlab.cn/install/

## 10.3 Git Lab安装

### 10.3.1 服务器准备

### 10.3.2 安装包准备

### 10.3.3 编写安装脚本

### 10.3.4 初始化GIt Lab服务

### 10.3.5 启动Git Lab服务

### 10.3.6 使用浏览器访问Git Lab

### 10.3.7 Git Lab创建远程仓库

### 10.3.8 IDEA集成Git Lab