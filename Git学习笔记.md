# Git学习笔记

## 版本控制

### 什么是版本控制

版本迭代，开发过程中，对项目各个阶段的版本的控制。

在开发过程中用于管理我们对文件、目录或工程等内容的修改历史，方便查看更改历史记录，备份以便恢复以前的版本。

多人开发必须要使用版本控制。

### 常见的版本控制工具

+ **Git**   （当下最流行）
+ **SVN**
+ **CVS**
+ **VSS**
+ **TFS**
+ Visual Studio Online

### 版本控制分类

#### 版本分类

1.本地版本控制

2.集中版本控制

3.分布式版本控制

#### 本地版本控制

记录文件每次的更新，可以对每个版本做一个快照，或是记录补丁文件，适合个人，如RCS。

#### 集中版本控制

所有的版本数据都保存在服务器上，协同开发者从服务器上同步更新或者上传自己的修改。例如，SVN、CVS、VSS。

所有的版本数据都存在服务器上，用户的本地只有自己以前同步的版本。不连网，用户看不到历史版本。

#### 分布式版本控制

所有版本信息仓库全部同步到本地的每个用户这样可以在本地查看所有历史版本，可以离线在本地提交，只需在连网时，将信息push到相应的服务器或其他用户那里。如Git

不会因为服务器损坏或者网络问题，造成不能工作的情况。

> SVN是集中式版本控制系统，版本库是集中放在中央服务器的。而工作的时候，用的都是自己的申脑。所以首先从中央服务器得到最新的版本，然后工作，完成工作后，需要把自己做完的活推送到中央服务器。集中式版本控制系统是必须联网才能工作，对网络带宽要求较高。
>
> Git是分布式版本控制系统，没有中央服务器。每个人的电脑就是一个完整的版本库，工作的时候不需要联网了。因为版本都在自己电脑上。协同的方法是这样的：比如说自己在电脑上改了文件A，其他人也在电脑上改了文件A，这时，你们两之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。Git可以直接看到了更新了哪些代码与文件。

## 常用Linux命令

### 基本的Linux命令

#### 改变目录

~~~bash
#返回上一级目录
cd ..

#切换目录
cd 目录路径+目录名
~~~

#### 显示目录

~~~bash
pwd
~~~

#### 清屏

~~~bash
clear
~~~

#### 列出当前目录下的文件

~~~bash
ls
~~~

#### 创建文件

~~~bash
#创建一个index.js
touch index.js
~~~

#### 删除文件

~~~bash
rm index.js
~~~

#### 新建目录

~~~bash
mkdir 文件目录名字
~~~

#### 删除目录

~~~bash
rm -r 文件目录名字
~~~

#### 移动文件

~~~bash
mv 目标对象 移动的位置
~~~

#### 查看历史命令

~~~bash
history
~~~

## Git的必要配置

### 查看配置的命令

~~~bash
#查看Git配置
git config -l

#查看系统配置
git config --system --list

#查看本地的一些配置
git config --global --list
~~~

### 设置邮箱和用户名

邮箱和用户名会被嵌入到所有的提交信息中，便于让别人知道是谁提交的

**必须配置**

~~~bash
git config --global user.name 用户名
git config --global user.email 邮箱
~~~

### 配置文件的位置

**所有的配置文件都在本地**

**Git的配置文件在：Git --> etc --> gitconfig**

## Git 的基本理论

### Git 工作区域

+ WorkSpace 工作区，平时存代码的地方（例如 Idea 项目文件所在位置）
+ Stage 暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交的文件列表信息 （项目中  .git  文件夹）
+ Repository  仓库，就是安全存放数据的位置，这里有你提交的所有版本的数据，其中HEAD 指向最新放入仓库的版本 

+ 远程仓库   Github 、Gitee（码云）

### Git的必要命令

~~~bash
#从工作区添加到暂存区（文件只是暂时保存，还没有永久化）
git add

#从暂存区提交到本地的Git仓库
git commit

#从本地仓库提交到远程仓库master分支
git push origin master
#推送到其他分支
git push origin dev

#从远程仓库把代码拉到本地
git pull

#从本地仓库回滚到暂存区
git reset

#从暂存区检出到工作区
git checkout
~~~

### Git 的工作流程

1.在目工作录中添加、修改文件

2.将需要进行版本管理的文件放入暂存区域 `git add .`

3.将暂存区的文件提交到git仓库 `git commit`

**git 管理的文件有三种状态：已修改、已暂存、已提交**

### 分支

**master** 主分支

#### 分支中常用的命令

~~~bash
#列出所有本地分支
git branch

#列出所有远程分支
git branch -r

#新建一个分支，但是依然停留在当前分支
git branch [branch-name]

#新建一个分支，并切换到新分支
git checkout -b [branch]

#合并指定分支到当前分支
git merge [branch]

#删除分支
git branch -d [branch-name]

#删除远程分支
git push origin --delete [branch-name]
git branch -dr [remote/branch]
~~~

+ 多个分支并行执行，就会导致我们代码不冲突，也就是同时存在多个版本
+ 如果合并分支时，同时修改了同一个文件，会引发冲突，需要协商
+ Master分支应该非常稳定，用来发布新版本，一般情况下不允许在上面进行操作

## Git项目搭建

### 本地仓库搭建

~~~bash
#第一种方法：进入项目的根目录，键入git init，会创建一个.git文件夹
git init

#第二种方法：克隆远程目录，将远程服务器上的仓库完全镜像一份至本地
#在Code-Clone-https内复制url,如 https://github.com/XuShengXianggg/Gitnotes.git
git clone [url]
~~~

## Git 文件操作

### 文件的四种状态

+ **未跟踪**：文件已经在文件夹中，但是还没有加入git仓库，通过**git add**状态变为 Staged

+ **未修改**：文件已经入库，且与项目文件内容一致。被修改，文件状态变为 **已修改**，如果使用 **git  rm** 移出仓库，则变为**未跟踪**。

+ **已修改**：文件已经修改。**git add --> 暂存状态；git checkout -->覆盖当前文件 --> 未修改。**

+ **暂存状态**：git commit --> 提交到仓库；git reset HEAD filename -->  取消暂存；

  

### 查看文件状态

~~~bash
#查看指定文件状态
git status [filename]

#查看所有文件状态
git status
~~~

### 修改文件状态

~~~bash
#添加所有文件到暂存区，将未跟踪状态转变为跟踪状态
git add .

#提交暂存区的内容到本地仓库
#  -m  提交信息
git commit -m "消息内容"
~~~

### 忽略文件

+ 有时候不需要把所有的文件都纳入版本控制，例如数据库文件、临时文件、设计文件等

+ 在**主目录**下建立  **".gitignore"**  文件，该文件有以下规则：

  1.文件中的注释#号开头

  2.可以使用Linux通配符

  3.如果名称**最前面**有一个感叹号！，表示例外规则，将不被忽略

  4.如果名称的**最前面**是一个路径分隔符/，表示要忽略的文件在此目录下，而子目录中的文件夹不忽略

  5.如果名称的**最后面**是一个路径分隔符/，表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）

~~~bash
#为注释
#忽略所有的  .txt  结尾的文件，这样的话上传不会被选中
*.txt       

#但是lib.txt除外（lib.txt不会被忽略）
!lib.txt

#仅忽略项目根目录下的TODO文件，但是不包括其他目录temp(/在前，忽略前面)
/temp

#忽略build目录下的所有文件（/在后，忽略后面）
build/

#会忽略 doc/notes.txt 但是不包括 doc/server/arch.txt
doc/*.txt
~~~

## 使用Gitee或者Github

### 使用流程

+ 注册登录码云，完善个人信息

+ 设置**本机绑定SSH公钥**，实现免密码登录

  ~~~bash
  #检查本地主机是否已经存在ssh key
  cd ~/.ssh
  ls
  #看是否存在 id_rsa 和 id_rsa.pub文件，如果存在，说明已经有SSH Key
  
  #在git命令窗口键入命令，创建公钥
  ssh-keygen -t rsa -C ”your_email@example.com“
  
  #获取公钥内容
  cd ~/.ssh
  cat id_rsa.pub
  
  #验证是否设置成功
  ssh -T git@github.com
  ~~~

  此时，一直回车继续，直到.ssh文件夹下出现类似  id_rsa.pub 和 id_rsa 文件

  将.pub文件的内容拷贝到码云或者Github的SSH公钥里面，生成认证信息

+ 使用Gitee或者Github新建一个仓库

  直接在Gitee或者Github新建一个远程仓库即可，将远程仓库克隆到本机

  ~~~bash
  git clone [url]
  ~~~

  **此处克隆的时候如果报错，例如...127.0.0.1  1136......，可能是你的git使用了代理，删除代理就好了**

  ~~~bash
  #删除代理
  git config --global --unset http.proxy
  ~~~

