# 玩转Git三剑客

# Git

- Git 官网：[https://git-scm.com](https://git-scm.com/)

- GitHub：[https://github.com](https://github.com/)

- GitLab：[https://about.gitlab.com](https://about.gitlab.com/)

- SVN：[https://subversion.apache.org](https://subversion.apache.org/)

---

## 01 | 版本管理理的演变

- VCS 出现前
用目录拷贝区别不同版本
公共文件容易被覆盖
成员沟通成本很高，代码集成效率低下

![image-20220429181114047](readme-image/image-20220429181114047.png)

---

- 集中式 VCS

有集中的版本管理理服务器，具备文件版本管理和分支管理能力
集成效率有明显地提高
客户端必须时刻和服务器器相连

![image-20220429181212223](readme-image/image-20220429181212223.png)

---

- 分布式 VCS

服务端和客户端都有完整的版本库脱离服务端，客户端照样可以管理理版本，查看历史和版本⽐比较等多数操作，都不不需要访问服务器器，比集中式 VCS 更能提高版本管理理效率

![image-20220429181438900](readme-image/image-20220429181438900.png)

---

- Git 的特点

最优的存储能力
非凡的性能
开源的
很容易做备份
支持离线操作
很容易定制工作流程

---

## 02 | 安装 Git

官⽹网安装指导
https://git-scm.com/book/en/v2/Getting-Started-Installing-Git 

检查安装结果，在 bash 下执⾏行行下⾯面的命令，看是否返回 git 的版本

```bash
$ git --version
git version 2.19.0
```

## 03丨git config 最小配置

最小配置,配置 user 信息

```bash
$ git config --global user.name ‘your_name’
$ git config --global user.email ‘your_email@domain.com’
```

config 的三个作⽤用域

缺省等同于 local

```bash
$ git config --local		## local只对仓库有效
$ git config --global		## global对登录⽤用户所有仓库有效
$ git config --system		## system对系统的所有⽤用户有效
```

显示 config 的配置，加 --list

```bash
$ git config --list --local
$ git config --list --global		## 常用
$ git config --list --system
```

设置与清除

> 设置，缺省等同于 local

```bash
$ git config --local
$ git config --global
$ git config --system
```

> 清除，--unset

```bash
$ git config --unset --local user.name
$ git config --unset --global user.name
$ git config --unset --system user.name
```

---

请动⼿⽐⼀⽐，local 和 global 的优先级。
1. 在 Git 命令⾏⽅式下，⽤ init 创建⼀个 Git 仓库。

  ```bash
  $ git init your_first_git_repo_name
  ```

2. cd 到 repo 中。

  ```bash
  $ cd your_first_git_repo_name
  ```

3. 配置 global 和 local 两个级别的 user.name 和 user.email。

  ```bash
  $ git config --local user.name 'your_local_name'
  $ git config --local user.email 'your_local_email@xxx.xxx'
  $ git config --global user.name 'your_local_name'
  $ git config --global user.name 'your_local_email@xxx.xxx'
  ```

4. 创建空的 commit

  ```bash
  $ git commit --allow-empty -m 'Initial'
  ```

5. ⽤ log 看 commit 信息，Author 的 name 和 email 是什么？

  ```bash
  $ git log
  ```

---



## 04丨git init 创建第一个仓库并配置local用户信息

两种场景：

1. 把已有的项目代码纳入git管理

```bash
cd your_project
git init
```

2. 新建的项目直接用git管理

```bash
cd xxx_dir
git init your_project
cd your_project
```

---

git init 实践：

```bash
## 项目初始化
$ git init git_learning
$ cd git_learning 
$ ls -la

## config --global 查看
$ git config --global --list
user.name=moox2020
user.email=1591112944@qq.com
credential.https://gitee.com.provider=generic

## config --local 设置
$ git config --local user.name 'moox_local'
$ git config --local user.email 'moox_local@163.com'
$ git config --local --list
user.name=moox_local
user.email=moox_local@163.com

## 将文件加入暂存区
$ touch readme.md
$ git add readme.md
$ git status
$ git commit -m "Add readme.md"
$ git log
commit 56513c9eed58960ca7d039a3816da25f8478346d (HEAD -> master)
Author: moox_local <moox_local@163.com>

```

这里的config 信息时 local配置的，说明local的优先级大于global

---

## 05丨 git add 暂存区 和 git commit 工作区

相关命令

```bash
git add file1 file2
git satus
git commit -m "xxx"
git log
git add -u 	## 将修改过的已被git管理的文件一次提交暂存区
```



- **往仓库里添加文件**

![image-20220428142126236](readme-image/image-20220428142126236.png)

实践：

```bash
../0-MATERIAL
|   index.html.01
|   index.html.02
|   readme
+---images
|       git-logo.png
+---js
|       script.js
\---styles
        style.css.01
        style.css.02

## 示例文件,页面访问： git_learning/index.html
$ cp ../0-material/index.html.01 index.html


$ cp -r ../0-material/images .
$ git add images index.html
$ mkdir styles
$ cp ../0-material/styles/style.css.01 styles/style.css
$ cp -r ../0-material/js/ .
$ git status
$ git add styles js
$ git commit -m "add styles + js"

## 在index.html 添加footer 信息
## 在style.css中添加 footer 信息

## 将已经被git管理的，但被修改过的文件一次提交到暂存区  -u
$ git add -u
$ git commit -m "add refering project"
$ git log
```

---

## 06丨git mv 给文件重命名的简便方法

相关命令

```bash
git mv readme reame.md
```

---

重命名已被git管理的文件

```bash
$ mv readme.md readme
$ git add readme
$ git rm readme.md
```

将上述操作复原，清理掉**暂存区**和**工作目录上的所有变更**

```bash
$ git status
...
        renamed:    readme.md -> readme
$ git reset --hard		## 将readme 还原为 readme.md文件
... 
		nothing to commit, working tree clean
$ git log	## git reset --hard 不会清理commit的内容
```

上述步骤一条命令实现：

```bash
$ git mv readme.md readme
        renamed:    readme.md -> readme
```

---

## 07丨git log 查看版本演变历史

- git log

```bash
$ git log 					## 查看所有log信息
$ git log --oneline			## 查看单行log
$ git log -n 2 --oneline	## -n 参数标识最近的几条commit信息，可以组合--oneline
```

- git branch -v  查看本地由多少分支

```bash
$ git branch -v				## 查看本地由多少分支
$ git branch -v
* master ed4a07e add readme -> readme.md

$ git checkout -b temp 242ba9de6208d4	## 创建分支，并切到分支
Switched to a new branch 'temp'

$ echo aa > readme.md
$ git commit -am "add test"
$ git branch -v
  master ed4a07e add readme -> readme.md
* temp   a255c07 add test

$ git log		## 查看当前分支log				
$ git log --all --graph --oneline -n 4		## 组合查看日志【--all 所有分支; --graph 带图形标识查看; -n 各分支最近】
```

---

## 08丨gitk：通过图形界面工具来查看版本历史

```bash
$ gitk		## 打开图形界面工具查看版本历史

## 注意在view -> new view -> all ref
```

还有很多功能

---

## 09丨.git 探密 cat-file\branch\checkout

本地实现版本管控系统，不需要远端支持

```bash
$ ll .git/
total 15
-rw-r--r-- 1 moox 197121   9 Apr 28 16:09 COMMIT_EDITMSG
-rw-r--r-- 1 moox 197121  21 Apr 28 16:08 HEAD			## 当前分支
-rw-r--r-- 1 moox 197121  41 Apr 28 15:48 ORIG_HEAD
-rw-r--r-- 1 moox 197121 184 Apr 28 14:08 config		## local config
-rw-r--r-- 1 moox 197121  73 Apr 28 14:03 description
-rw-r--r-- 1 moox 197121 546 Apr 28 16:20 gitk.cache
drwxr-xr-x 1 moox 197121   0 Apr 28 14:03 hooks/
-rw-r--r-- 1 moox 197121 336 Apr 28 16:09 index
drwxr-xr-x 1 moox 197121   0 Apr 28 14:03 info/
drwxr-xr-x 1 moox 197121   0 Apr 28 14:15 logs/
drwxr-xr-x 1 moox 197121   0 Apr 28 16:09 objects/		## 文件信息
drwxr-xr-x 1 moox 197121   0 Apr 28 14:03 refs/			## 存放分支及tag等信息
```

---

- HEAD

```bash
$ cat .git/HEAD
ref: refs/heads/temp		## 保存引用的当前分支名称

$ git branch -av
  master ed4a07e add readme -> readme.md
* temp   a255c07 add test	## 当前分支

$ git checkout master		## 分支切到master
Switched to branch 'master'

$ git branch -av
* master ed4a07e add readme -> readme.md	## 当前分支为 master
  temp   a255c07 add test

$ cat .git/HEAD
ref: refs/heads/master		## 内容已经修改
```

---

- config，存放本地仓库的配置信息

```bash
$ cat .git/config
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
[user]
        name = moox_local
        email = moox_local@163.com
```

可以单独查看每个配置项

```bash
$ git config --local --list 				## 查看所有local
$ git config --local user.name 'moox2020'	## 设置值
$ git config --local user.name				## 查看单值
```

---

- refs

```bash
$ ls .git/refs/
heads/  		## 对应分支
tags/			## 对应版本，里程碑

## 
$ cat .git/refs/heads/master
ed4a07eaddf6e7a9fe3ae1a36383fc7ad5f113bf   ## master commit 的hash

## 
$ git cat-file -t ed4a07e
commit

## 查看分支
$ git branch -av
* master ed4a07e 
  temp   a255c07

$ cat .git/refs/heads/temp
a255c07f9a6c8aa7597ed0e2f1ba23a757996933		## temp commit 的hash

$ git cat-file -t a255c07f9a6c8		## 查看hash对应的类型，如 commit,tag
$ git cat-file -p a255c07f9a6c8		## 查看hash对应的内容
```

---

- objects，保存文件的hash

```bash
## blob
$ ll .git/objects/ef/3f137d8af338a8604544a3e482090684321d93
-r--r--r-- 1 moox 197121 322 Apr 28 15:22 .git/objects/ef/3f137d8af338a8604544a3e482090684321d93
$ git cat-file -t ef3f137d8af338a8604544a3e482090684321d93		## 文件夹+hash
blob		## blob为文件类ing
$ git cat-file -p ef3f137d8af338a8604544a3e482090684321d93		## 查看文件内容

## tree
$ git cat-file -t c033b66b08d2ef27509b0cc40706b011346786f5
tree
moox@LAPTOP-3K47INF5 MINGW64 /d/moox/sanwei-bookstore/git/git_learning (master)
$ git cat-file -p c033b66b08d2ef27509b0cc40706b011346786f5
040000 tree 96b67e399c8496ec36cbbbcb776eb924fad7f9a7    images
```

---

## 10丨commit、tree和blob三个对象之间的关系

- 一个commit 对应一棵树tree，表示当前仓库的状态镜像，tree中包含tree和blob
- tree , 表示文件夹 hash， tree 中递归包含 tree，blob
- blob , 表示文件 hash

![image-20220428200201603](readme-image/image-20220428200201603.png)

实践：

```bash
$ git branch -av			## 查看分支信息
* master ed4a07e add readme -> readme.md
  temp   a255c07 add test

$ git cat-file -t ed4a07e	## 查看commit 
commit

$ git cat-file -p ed4a07e	## 查看内容，包含tree
tree 1fa0ab83fd0d2bcaa93dc9f23ad6cc413282797d

$ git cat-file -p 1fa0ab83fd0d2bcaa93dc9f23ad6cc413282797d	## 继续查看树
040000 tree 96b67e399c8496ec36cbbbcb776eb924fad7f9a7    images
100644 blob 193265d0bf242c63ad8aedf38f81552d204f84ee    index.html
...
$ git cat-file -p 40830374235df1c19661a2901b7ca73cc9499f3d	## 查看文件内容
```

---

## 11丨tree 的个数

> 新建的Git仓库，有且仅有1个commit，仅仅包含 /doc/readme ，请问内含多少个tree，多少个blob？

![image-20220428204157076](readme-image/image-20220428204157076.png)

```bash
$ git init watch_git_objects
$ cd watch_git_objects
$ mkdir doc -pv
$ echo hello,world > doc/readme

## git add
$ git add doc						## 将文件加放入暂存区，就会有object创建出来
$ find .git/objects/ -type f
.git/objects/2d/832d9044c698081e59c322d5a2a459da546469		## 这里只有1个文件
$ git cat-file -t 2d832d9044c698081e59c322d5a2a459da546469	## 类型
blob
$ git cat-file -p 2d832d9044c698081e59c322d5a2a459da546469	## 内容
hello,world

## git commit 
$ git commit -m "Add readme"
$ find .git/objects/ -type f								## 这里有4个文件
.git/objects/04/117656abf05874da05f7b70dcea87c8cef7ee4		## type: commit
.git/objects/08/3e18d286d8d2a9eda8c62d9d98935dcc07ca4c		## type: tree; content: doc(tree)
.git/objects/2d/832d9044c698081e59c322d5a2a459da546469		## type: blob, hello,world
.git/objects/ba/8711bd7540faa22e4e76a1cf5c78501fa4e162		## type: tree, readme(blob)

## 说明：
commit 	-> 	(tree doc)
doc 	->  (tree readme)
readme 	-> 	(blob)
```

---

## 12丨HEAD detached 分离头指针情况下的注意事项

> 使用场景，有时候想要做一些变更，但不想影响整个分支，这时候可以切到某个log，分离头指针，这时候的变更式没有分支的，即使变更错了也没关系，切到其他分支即可。

实践：

```bash
$ cd git_learning/
$ git log
commit 48cf442dfeb5873004267d4759ca0a8fbd8c8bd8
...
    add style.css
$ git branch
* (HEAD detached at 48cf442)		## 分离头指针，不跟分支挂钩，会被当做垃圾收拾掉
  master
  temp

## 修改文件信息    
$ vim styles/style.css
	background-color: green;
$ git commit -am "Background to green"		## -am 直接提交，不放到暂存区，不推荐
$ git log
commit 5f62afaaae649d699e433c575366ca184fcb76a2 (HEAD)	## 这里没有绑定分支，只有HEAD，表示分离头指针
    Background to green

## checkout 到其他分支，提醒信息：
$ git checkout master
Warning: you are leaving 1 commit behind, not connected to
any of your branches:
  5f62afa Background to green
If you want to keep it by creating a new branch, this may be a good time
to do so with:
 git branch <new-branch-name> 5f62afa
Switched to branch 'master'

## 查看有没有在合上分支
$ gitk --all			## view全选上也发现没有该分支
## 如果修改是重要的，可以修复：git branch <new-branch-name> 5f62afa
$ git branch fix_css 5f62afa
$ git branch -av
  fix_css 5f62afa Background to green		## 这里能看到分支
* master  ed4a07e add readme -> readme.md
  temp    a255c07 add test
$ gitk --all			## view全选上发现有该分支
```

---

## 13丨git diff 进一步理解HEAD和branch

新分支创建后，head是怎样的？

实践：

```bash
## 查看当前分支
$ git branch -av
  fix_css 5f62afa Background to green
* master  ed4a07e add readme -> readme.md
  temp    a255c07 add test
## 基于 fix_css 创建新分支，并切换到新分支fix_readme
$ git checkout -b fix_readme fix_css
Switched to a new branch 'fix_readme'
## 查看历史版本信息，HEAD指向了基于fix_css的新分支fix_readme
$ git log -n1
commit 5f62afaaae649d699e433c575366ca184fcb76a2 (HEAD -> fix_readme, fix_css)
$ gitk --all
```

![image-20220428213102864](readme-image/image-20220428213102864.png)

---

- 分支最终会落脚到某个commit

```bash
$ cat .git/HEAD
ref: refs/heads/fix_readme
$ cat .git/refs/heads/fix_readme
5f62afaaae649d699e433c575366ca184fcb76a2
$ git cat-file -t 5f62afaaae649d699e433c575366ca184fcb76a2
commit
```

- commit 之间比较差异

> head 为最新的commit
>
> head^ = head^1 = head ~1 = 上一个commit
>
> head^^ = head^^2 = head ~2 = 上上个commit

```bash
## 简单比较
$ git diff head head^
diff --git a/styles/style.css b/styles/style.css
index 4c6bc45..ef3f137 100644
--- a/styles/style.css
+++ b/styles/style.css
@@ -1,5 +1,5 @@
 body{
-  background-color: green;
+  background-color: orange;

## 比较原理，就是两个commit hash比较，因为head中保存的就是commit信息
$ git diff  5f62afaaae649d699e433c575366ca184fcb76a2 48cf442dfeb5873004267d4759ca0a8fbd8c8bd8
diff --git a/styles/style.css b/styles/style.css
index 4c6bc45..ef3f137 100644
--- a/styles/style.css
+++ b/styles/style.css
@@ -1,5 +1,5 @@
 body{
-  background-color: green;
+  background-color: orange;
   font-family: 'Monaco', sans-serif;
   color: white;
 }
```

---

## 14丨git branch -d | -D 删除不需要的分支

```bash
$ git branch -av
  fix_css    5f62afa Background to green
* fix_readme 5f62afa Background to green		## 所在分支，不能删除
  master     ed4a07e add readme -> readme.md
  temp       a255c07 add test
## 先切换到其他分支
$ git checkout master
Switched to branch 'master'

## -d 删除分支，提醒不能删除
$ git branch -d fix_readme
error: The branch 'fix_readme' is not fully merged.
If you are sure you want to delete it, run 'git branch -D fix_readme'.

## -D 删除分支
$ git branch -D fix_readme
Deleted branch fix_readme (was 5f62afa).

## 查看已删除分支
$ git branch -av
  fix_css 5f62afa Background to green
* master  ed4a07e add readme -> readme.md
  temp    a255c07 add test
```

---

## 15丨git commit --amend 修改最新commit msg

> 对最近一次提交的msg 做变更

```bash
moox@LAPTOP-3K47INF5 MINGW64 /d/moox/sanwei-bookstore/git/git_learning (master)
$ git branch -av
* master  ed4a07e add readme -> readme.md			## commit msg = "add readme -> readme.md"

## 修改commit msg
$ git commit --amend
[master 76f7871] move filename readme to readme.md

$ git branch -av
* master  76f7871 move filename readme to readme.md	## commit msg = "move filename readme to readme.md"

$ git log -n1
commit 76f78710be62c17ebf2ecad16ab73512c8c58850 (HEAD -> master)
    move filename readme to readme.md

```

---

## 16丨rebase reword 修改老旧commit的msg

```bash
$git branch -av			## 当前分支 master
* master  76f7871 move filename readme to readme.md		## master 76f7871

$ git log -n4				## 最近三次的commit
commit 76f78710be62c17ebf2ecad16ab73512c8c58850 (HEAD -> master)
    move filename readme to readme.md
commit f2b6a1c22d4bd03687b67f210a70bdd3f8154aed
    add readme.md -> readme
commit 8851bb716621dd7f2ef7988028ad24ed78d3d167		## 假设需要修改旧的这个commit
    add refering project
commit f3db4f662775a570d3489b329090810ac53f9072		## 需要使用被修改的commit的父commit作为变更基准
    add js

## git rebase -i 交互式变基
$ git rebase -i f3db4f662775a
## 第1次弹出交互式窗口是这次变更的msg内容

pick 8851bb7 add refering project ## 将pick 修改为r
r 8851bb7 add refering project
## 第2次弹出交互式窗口是这次变更的原因信息msg

$ git branch -av
* master  c444716 move filename readme to readme.md		## ## master 76f7871 树变了

$ git log -n 4 --graph
## 能看到commit msg 已经变了
```

---

## 17丨rebase squash 把连续的多个commit合并

将连续的多个commit合并为1个commit

```bash
$ git log
commit c181995088168d22f1248ead2dbfe7e8246242f1  (下面3个合并到这个)
    add refering a project
commit f3db4f662775a570d3489b329090810ac53f9072	（3）
    add js
commit 48cf442dfeb5873004267d4759ca0a8fbd8c8bd8	（2）
    add style.css
commit 242ba9de6208d4f4336a99d59fdc04f5b4740601	（1）
    Add index + logo
commit 56513c9eed58960ca7d039a3816da25f8478346d	（使用这个作为base）
    Add readme.dm

$ git rebase -i 56513c9eed58
pick 242ba9d Add index + logo
s 48cf442 add style.css
s f3db4f6 add js
s c181995 add refering a project
pick 1ed2c5b add readme.md -> readme

# s, squash <commit> = use commit, but meld into previous commit
# s 表示压缩，将连续的commit合并提交

# This is a combination of 4 commits. 添加如下内容
Create a complete web page.

## 查看日志，历经合并了
$ git log --graph
* commit 261a6e2cee0a43d3a81eee58c8ea268bf0fec643 (HEAD -> master)
|     move filename readme to readme.md
|
* commit 3c9df966894f7930ac6f578cbc8000870dbc47ee
|     add readme.md -> readme
|
* commit b6c69b1bb8b7ca408f0b54b379dd9e3c6748348e
|     Create a complete web page.
|     Add index + logo
|     add style.css
|     add js
|     add refering a project
|
* commit 56513c9eed58960ca7d039a3816da25f8478346d
      Add readme.dm
```

---

## 18丨rebase squash  把间隔的多个commit合并

上述中，多个commit都有readme，且commit不连续，这里将其合并为一个readme

```bash
## 原来的信息
pick b6c69b1 Create a complete web page.
pick 3c9df96 add readme.md -> readme
pick 261a6e2 move filename readme to readme.md

## 添加新合并的内容，并调整顺序
pick 56513c9eed58960c
s 3c9df96 add readme.md -> readme
s 261a6e2 move filename readme to readme.md
pick b6c69b1 Create a complete web page.

## 这里保存时会直接退出，提示：git commit --allow-empty，可以查看状态
$ git status
You are currently rebasing branch 'master' on '56513c9'.
  (all conflicts fixed: run "git rebase --continue")
  
$ git rebase --continue
# This is a combination of 3 commits.
Add readme.md
...

## 这时候就已经把readme相关的commit合并了
$ git log --graph
* commit 4477817c1388403b3e899de9c5c94622435a9f37 (HEAD -> master)
|     Create a complete web page.
|     Add index + logo
|     add style.css
|     add js
|     add refering a project
* commit 9d678d51c80c6e7c4fc53ca3d8a3a73dc8e1a56c
      Add readme.md
      Add readme.dm
      add readme.md -> readme
      move filename readme to readme.md
      
## 查看树结构
$ gitk --all
```

---

## 19丨git diff --cached 比较暂存区和HEAD所含文件

![image-20220429123613750](readme-image/image-20220429123613750.png)

> 将暂存区的文件与最近一次已经提交的文件(HEAD=历史版本)做一次比较差异，再确定是否commit

```bash
$ vim index.html
$ git add -u
$ git status
$ git diff --cached
diff --git a/index.html b/index.html
...
-                    <li></li>
+                    <li>add</li>

$ git commit -m "Add the first command with config"
```

---

## 20丨git diff -- 比较工作区和暂存区所含文件的差异？

- 这里的比较都是工作区和暂存区的同文件名比较

```bash
$ vim index.html				#  <li>bare repositry</li>
$ git add index.html
$ vim styles/style.css			#  color: white; => black
$ vim readme.md					#  hello world.

## -- 可以不加
$ git diff									## 工作区和暂存区所有文件比较
$ git diff -- readme.md						## 比较指定文件
$ git diff -- readme.md styles/style.css	## 指定多个文件
$ git diff styles/							## 指定目录下的所有文件比较
```

---

## 21丨 git restore --staged 让所有暂存区 -> HEAD 一致

暂存区的所有信息不保留，Head就是已经提交了的信息。让暂存区与Head一致，就是删除暂存区数据即可

- head不变，处理暂存区
- 早期使用git reset = git restore --staged 

```bash
$ git status
(use "git restore --staged <file>..." to unstage)		## git restore --staged将暂存区的文件与head一致

## 必须指定path， . 表示所有
$ git restore --staged .		## 将暂存区与Head一致（以head为基准）

## 比较暂存区和Head ，
$ git diff --cached						## 暂存区与head比较
no changes added to commit (use "git add" and/or "git commit -a")

```

---

## 22丨git restore 让所有工作区 -> 暂存区 一致

- 暂存区不变，处理工作区
- git restore 将工作区的文件与暂存区一致

 ```bash
$ git status
  (use "git restore <file>..." to discard changes in working directory)
  
$ git restore .	 ## 将工作区与暂存区文件保持一致（暂存区为基准）

$ git diff 		## 工作区与暂存区比较
 ```

---

## 23丨git restore --staged file... 取消暂存区部分文件

暂存区的部分信息不保留，Head就是已经提交了的信息。让暂存区与Head一致，就是删除暂存区指定数据即可

- head不变，处理暂存区
- 早期使用git reset = git restore --staged file...

```bash
$ git status
(use "git restore --staged <file>..." to unstage)		## git restore --staged将暂存区的文件与head一致

## 必须指定path， . 表示所有
$ git restore --staged index.html readme.md		## 将暂存区与Head一致（以head为基准）

## 比较暂存区和Head 
$ git diff --cached						## 暂存区与head比较
no changes added to commit (use "git add" and/or "git commit -a")
```

---

## 24丨git reset --hard 消除最近的几次commit

- 暂存区和工作区的变更都会被取消掉，是一条危险的命令

```bash
$ git branch -av
  fix_css 5f62afa Background to green
  master  fc60d2c Add the first command with config
* temp    a255c07 add test

$ git log
commit a255c07f9a6c8aa7597ed0e2f1ba23a757996933 (HEAD -> temp)
    add test
commit 242ba9de6208d4f4336a99d59fdc04f5b4740601   ## 回到这个commit
    Add index + logo
commit 56513c9eed58960ca7d039a3816da25f8478346d
    Add readme.dm

## 回到指定的commit，最近的几次都会被清除（包含工作区和暂存区）
$ git reset --hard 242ba9de6208d4f
```

---

## 25丨git diff 查看不同commit 之间的差异

- 比较不通commit之间的差异

```bash
## 比较两个commit的全部文件差异，master和temp表示两个不同分支最新的commit
$ git diff master temp

## 比较两个不通分支最新commit的指定文件差异
$ git diff master temp  -- index.html

## 指定任意两个commit之间的差异
$ git diff fc60d2c 242ba9d 					## 两个commit之间全部差异
$ git diff fc60d2c 242ba9d -- index.html	## 两个commit之间指定的文件差异
```

---

## 26丨git rm 删除文件的方法

- 指定文件删除和恢复
- 不指定文件时，使用 .  表示所有文件
- 可以直接操作暂存区。因为删除暂存区文件，工作区也会被删除。可以通过Head恢复

```bash
## 指定文件删除和恢复
$ rm readme.md				## 工作区删除文件
$ git restore readme.md		## 从暂存区恢复到工作区

$ rm readme.md						## 工作区删除文件
$ git rm readme.md					## 暂存区删除文件
$ git restore --staged readme.md	## 从Head 恢复文件到暂存区
$ git restore readme.md				## 从暂存区恢复文件到工作区

## 全部删除和恢复
$ git restore --staged .			## 从Head 恢复全部文件到暂存区
$ git restore . 					## 从暂存区恢复全部文件到工作区

## 推荐做法
$ git rm readme.md 					## 同时删除暂存区和工作区文件
$ $ git reset --hard head			## 从Head恢复文件到暂存区和工作区，也可以使用restore分步完成
```

---

## 27丨git stash 处理临时加塞的紧急任务

场景：部分文件在工作区，部分文件在暂存区（stage)，临时紧急需要修复Head 的bug , 工作路径需要改为head

处理逻辑：先将暂时的工作放到另一个区域中，处理完紧急bug，再恢复临时工作

- 使用stash保存临时工作，git stash
- 出栈恢复之前的工作，并保持栈内容，git stash apply
- 出栈恢复之前的工作，删除栈中内容，git stash pop

```bash
$ git status			## 临时工作
        modified:   index.html

$ git stash			## 工作区临时存放到stash，堆栈中
Saved working directory and index state WIP on master: fc60d2c Add the first command with config

$ git stash list	## 查看堆栈
stash@{0}: WIP on master: fc60d2c Add the first command with config

$ git status		## 这时候工作区是清空的
On branch master
nothing to commit, working tree clean

## 处理紧急事项，如修改index.html
.... 修改完成

$ git stash apply		## 从stash栈中恢复之前的工作，同时保存stash的信息，之后依然可用
$ git stash list		## 能看到stash中仍然还有
$ git status			## 已恢复临时工作状态

$ git reset --hard head	## 清空工作区
$ git status
On branch master
nothing to commit, working tree clean

$ git stash list		## stash
stash@{0}: WIP on master: fc60d2c Add the first command with config

$ git stash pop			## 出栈，栈中信息出栈后就被删除Dropped
...
        modified:   index.html
Dropped refs/stash@{0} (317e65b54ba6bc569d0042f18e994bf607a552f6)
```



---

## 28丨gitignore 指定不需要Git管理的文件

> https://github.com/github/gitignore

指定不需要git管理的文件

实践：

```bash
$ mkdir doc							## doc 目录
$ echo aa > doc/readhim	
$ echo "this is a file " > doc		## doc 文件

$ vim .gitignore
doc					## 表示忽略 doc 文件和目录
doc/				## 只忽略doc/ 目录下的文件，不会忽略doc文件
```

---

## 29丨git clone  将Git仓库备份到本地

- 常⽤用的传输协议
  - 哑协议与智能协议， git clone 
    - 直观区别：哑协议传输进度不不可⻅见；智能协议传输可⻅见。
    - 传输速度：智能协议⽐比哑协议传输速度快。
- 与远端关联
  - git remote

![image-20220429172047882](readme-image/image-20220429172047882.png)

---

- 备份特点：多点备份

![image-20220429172152041](readme-image/image-20220429172152041.png)

---

- 哑协议和智能协议 实践：

```bash
$ pwd
/git/666-backup

## --bare  clone不带工作区的裸仓库
$ git clone --bare /git_learning/.git ya.git		##哑协议
Cloning into bare repository 'ya.git'...
done.

## 智能协议(有进度条及压缩等功能，推荐)
$ git clone --bare file:///git_learning/.git zhineng.git		## file://
Cloning into bare repository 'zhineng.git'...
remote: Enumerating objects: 27, done.
remote: Counting objects: 100% (27/27), done.
remote: Compressing objects: 100% (20/20), done.
remote: Total 27 (delta 8), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (27/27), 21.99 KiB | 1.22 MiB/s, done.
Resolving deltas: 100% (8/8), done.
```

---

- 与远端关联，将本地变更同步到远端

```bash
$ cd /git/git_learning
$ git remote -v				## 查看是否已关联远端分支，没有时新建远端分支

$ git remote add zhineng   file:///git/666-backup/zhineng.git/

$ git remote -v				## 关联上了
zhineng file:///git/666-backup/zhineng.git (fetch)
zhineng file:///git/666-backup/zhineng.git (push)

$ git branch -av
  fix_css                5f62afa Background to green
* master                 0251ee0 text.txt
  temp                   242ba9d Add index + logo
  remotes/zhineng/master fc60d2c Add the first command with config	## 这里包含了远端的分支

$ git push zhineng		## 提交到远端分支
```

---

# GitHub

## 30丨GitHub账号注册

> https://github.com/ 

- 注册(用户名，注册邮箱)
- read the guide 
- start a project
- new repositry
- 右上角
  - your profile  , 个人信息
  - Help，帮助信息 -> https://docs.github.com/cn 

---

## 31丨GitHub配置公私钥

> 在GitHub的Help中搜索：ssh ->  Connecting to GitHub with SSH
>
> https://docs.github.com/en/authentication/connecting-to-github-with-ssh 

Connecting to GitHub with SSH， 添加ssh key 到GitHub帐号
- [About SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh)

- [Checking for existing SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)

- [Adding a new SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)  


---



Checking for existing SSH keys

```bash
$ mkdir ~/.ssh && cd ~/.ssh 
$ ls -al ~/.ssh
## 不存在则创建 
```

Generating a new SSH key 

```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
$ ll
total 8
-rw-r--r-- 1 moox 197121 3381 Apr 29 19:13 id_rsa
-rw-r--r-- 1 moox 197121  743 Apr 29 19:13 id_rsa.pub
$ cat id_rsa.pub
... 公钥内容

```

Adding a new SSH key to your GitHub account

- In the upper-right corner of any page, click your profile photo, then click **Settings**.
- In the "Access" section of the sidebar, click **SSH and GPG keys**.
- Click **New SSH key** or **Add SSH key**.

---



## 32丨GitHub上创建个人仓库

- In the upper-right corner of any page, click your "+"：**New Repository**.
- Repository Name
- Description (optional) ，仓库搜索时可能被检索到
- Public / Private，可见性
- Initialize this repository with:
  - Add a README file（项目没有readme时，建议选上）
  - Add .gitignore（可选）
- Choosing the right license（可选）

---



## 33丨git push 把本地仓库同步到GitHub

- 本地仓库

```bash
$ pwd
/git/git_learning
$ git remote -v
zhineng file:///git/666-backup/zhineng.git (fetch)
zhineng file:///git/666-backup/zhineng.git (push)
```

- 新增远端站点

> github仓库中选择ssh的git

```bash
## 格式：git remote add git_name git_repository
$ git remote add github git@github.com:moox2020/git_learning.git

$ git remote -v
github  git@github.com:moox2020/git_learning.git (fetch)
github  git@github.com:moox2020/git_learning.git (push)

$ git push github --all		## 所有分支全部push到github
$ git fetch github master	## 拉去远端仓库，不合并
$ git merge github/master	## 与远端master合并，可以添加--allow-unrelated-histories，不相关也合并
$ git push github master	## 将本地分支master push 到GitHub
```

---



## 34丨git merge 处理不同user修改的不同文件

> 结论：不通文件，合并处理

```bash
git branch -v            	// 查看本地分支
git branch -av           	// 查看本地及远端分支
git getch repo    		 	// 拉取仓库
git  checkout -b a repo/a	//基于repo/a 分支，创建本地分支a
git merge  repo/xxx			//合并分支
```

github 上添加一个分支 feature/add_git_commands 

```bash
##  git_learning 中的user
$ pwd
/git/git_learning
$ git config --local --list
user.name=moox_local
user.email=moox_local@163.com

##  git_learning_02 中的user
$ cd ..
$ git clone git@github.com:moox2020/git_learning.git git_learning_02
$ cd git_learning_02
$ git config --local --list
$ git config --add --local user.name "moox2020"
$ git config --add --local user.email "moox2020@163.com"

$ git branch -av
  remotes/origin/feature/add_git_commands 0251ee0 text.txt

## 基于远端的分支，创建本地分支，并切到该分支
$ git checkout -b feature/add_git_commands origin/feature/add_git_commands
Switched to a new branch 'feature/add_git_commands'
branch 'feature/add_git_commands' set up to track 'origin/feature/add_git_commands'.

$ vim readme.md
$ git add -u
$ git commit -m "Add git commands description in readme"
$ git push

## github可以看到commit的user信息
```

切换到另一个仓库git_learning，fetch分支

```bash
$ cd ../git_learning		## 这个仓库没有remotes/github/feature/add_git_commands
$ git branch -av
  fix_css                5f62afa Background to green
* master                 0251ee0 text.txt
  temp                   242ba9d Add index + logo
  remotes/github/fix_css 5f62afa Background to green
  remotes/github/main    2ecdc98 Initial commit
  remotes/github/master  0251ee0 text.txt
  remotes/github/temp    242ba9d Add index + logo
  remotes/zhineng/master 0251ee0 text.txt

## fetch 远端
$ git fetch github
 * [new branch]      feature/add_git_commands -> github/feature/add_git_commands

## 基于远端创建分支
$ git checkout -b feature/add_git_commands github/feature/add_git_commands
$ vim index.html						## 修改文件内容
$ git add index.html
$ git commit -m "Add info to index"		## commit 但不push到remote
```

换到仓库：git_learning_02

```bash
$ cd ../git_learning_02/
$ vim readme.md
$ git commit -am "Add here in readme"
```

切回仓库：git_learning

```bash
$ cd ../git_learning
$ git push								## git push 报错了
To github.com:moox2020/git_learning.git
 ! [rejected]        feature/add_git_commands -> feature/add_git_commands (fetch first)
error: failed to push some refs to 'github.com:moox2020/git_learning.git'

## 先fetch
$ git fetch	
$ git branch -av
* feature/add_git_commands                85c0034 [ahead 1, behind 1] Add info to index
## [ahead 1, behind 1], 我有一个commit，远端没有；远端有一个commit，我没有；

## 合并，如果修改的不是同一个文件，可以合并
$ git merge github/feature/add_git_commands

## 
$ git push
```

---



## 35丨git merge处理不同user修改同一文件不同区域

> 结论：同一文件，不同区域，合并处理

在仓库git_learning 和 仓库 git_learning_02 中同时修改index.html 

- git_learning

```bash
## 操作前将仓库与远端仓库同步,并更新本地仓库
$ git pull 
$ vim index.html			## 这里修改第3行
$ git add -u
$ git commit -m "Add git_learnging in index"
```

- git_learning_02

```bash
## 操作前将仓库与远端仓库同步,并更新本地仓库
$ git pull 
$ vim index.html			## 这里修改第14行
$ git add -u
$ git commit -m "Add git_learnging_02 in index"
$ git push
```

- 回到git_learning push

```bash
$ git push
To github.com:moox2020/git_learning.git
 ! [rejected]        feature/add_git_commands -> feature/add_git_commands (fetch first)
error: failed to push some refs to 'github.com:moox2020/git_learning.git'

$ git fetch github
$ git merge github/feature/add_git_commands		## 与远端分支合并
$ git push	## 再次push OK
```

---

## 36丨git merge处理不同user修改同一文件同一区域

> 结论：同一文件，同一区域，git不能合并处理，需要人为介入

| repo git_learning                                            | repo git_learning_02                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| git pull github                                              | git pull github                                      |
| 修改index.html 相同行                                        | 修改index.html 相同行                                |
| git commit -am 'add command rm and mv in index'              | git commit -am 'add commands stash and log in index' |
|                                                              | git push  github   ==> 先push ok                     |
| git push github  ==> rejected(fetch first)                   |                                                      |
| $ git fetch github  ==> [ahead 1, behind 1]                  |                                                      |
| $ git merge github/feature/add_git_commands ==>CONFLICT      |                                                      |
| **人工介入商讨修改修改index.html内容<br />- 合并：git commit <br />- 不合并：git merge --abort** |                                                      |
| $ git commit -am 'resolve merge and all include in index'    |                                                      |
| $ git push github                                            |                                                      |

---



## 37丨git merge处理同时变更了文件名和文件内容

> 结论：不同user修改同一文件的文件名和文件内容，不影响分支合并push

| repo git_learning                               | repo git_learning_02                               |
| ----------------------------------------------- | -------------------------------------------------- |
| git pull github                                 | git pull github                                    |
| git mv index.html index.htm                     | vim index.html                                     |
| git commit -am 'rename index.html to index.htm' | $ git commit -am 'update the head in index'        |
| git push  github ==> ok                         |                                                    |
|                                                 | git push github  ==> rejected(fetch first)         |
|                                                 | $ git fetch github  ==> [ahead 1, behind 1]        |
|                                                 | $ git merge github/feature/add_git_commands ==> OK |
|                                                 | git push github ==> OK                             |
| 新的文件名，新的内容                            | 新的文件名，新的内容                               |

---

## 38丨git pull 处理同一文件被改成不同的文件名

| repo git_learning                                            | repo git_learning_02                          |
| ------------------------------------------------------------ | --------------------------------------------- |
| git pull github                                              | git pull github                               |
| git mv index.htm index1.html                                 | git mv index.htm index2.html                  |
| git commit -am ' Mv index.htm to index1.html'                | git commit -am ' Mv index.htm to index2.html' |
|                                                              | git push github  => Ok                        |
| git push github => rejected                                  |                                               |
| **git pull github   => 拉取remote repo，同时auto merge**     |                                               |
| ls 查看本地同时存在两个文件：index1.html 和index2.html       |                                               |
| $ diff index1.html index2.html   ==> 文件内容一样，文件名不同 |                                               |
| git status 查看状态：<br />both deleted:    index.htm<br/>added by them:   index1.html<br/>added by us:     index2.html |                                               |
| 人工介入决定 使用index1.html                                 |                                               |
| git rm index.htm<br />git rm index2.html<br />git add index1.html |                                               |
| $ git commit -am 'decided to mv index.htm to index1.html'    |                                               |
| $ git push github   ==> ok                                   |                                               |

---

## 39丨(禁止)--force / -f 强制向集成分支执行push操作

```bash
$ git log --oneline								## 能看到很多历史commit记录
$ git reset --hard fc60d2c						## 重置指向历史的某个commit
$ git push  -f github feature/add_git_commands	## 强制提交到remote，github是repoName,默认为origin
$ git log --oneline								## fc60d2c 到最新的commit都没了... 啪啪啪
## 远端的commit记录也没有了，因此禁止执行 git push  -f
```

---

## 40丨(禁止)向集成分支执行变更历史的操作

---



## 41丨Why GitHub

- Git诞生之前

![image-20220430115612009](readme-image/image-20220430115612009.png)

---

- Git诞生之后

![image-20220430115739488](readme-image/image-20220430115739488.png)

---

- GitHub诞生了

![image-20220430115822391](readme-image/image-20220430115822391.png)

---

- GitHub的10年

![image-20220430115943215](readme-image/image-20220430115943215.png)

---

- Github成功的因素

![image-20220430120039290](readme-image/image-20220430120039290.png)

---



## 42丨GitHub 核心功能

> https://github.com/features
>
> https://github.com/marketplace

- Collaborative Coding
- Automation & CI/CD
- Security
- Client Apps
- Project Management
- Team Administration
- Community

---

## 43丨GitHub Search

GitHub搜索，查询的是repo Name 和 repo Descriptions

https://github.com/search/advanced 

https://docs.github.com/en/search-github/searching-on-github  

```bash
created:>2022-04-29						## 仓库创建时间
git learning in:readme					## readme.me 文件中包含关键字
git learning in:readme starts:>1000		## 组合搜索
...
## https://docs.github.com/en/search-github/searching-on-github  
Finding files on GitHub
Searching for repositories
Searching topics
Searching code
Searching commits
Searching issues and pull requests
Searching discussions
Searching GitHub Marketplace
Searching users
Searching for packages
Searching wikis
Searching in forks
```

---



## 44丨GitHub上搭建个人博客

搜索：blog easily start in:readme stars:>5000

- https://github.com/barryclark/jekyll-now

- Step 1) Fork Jekyll Now to your User Repository

  ​	**Fork** this repo, then **rename** the repository to **yourgithubusername.github.io**

- Step 2) Customize and view your site

  ​	Enter your site name, description, avatar and many other options by **editing the _config.yml** file. 

  - name: moox2020

-  Step 3) Publish your first blog post

  ​	Edit `/_posts/2014-3-3-Hello-World.md` to publish your first blog post. 

  - 文件格式：date-content.md  ==> 2014-3-3-Hello-World.md
  - create new file : 2022-04-40-moox2020-firstblog.md (随意内容)



45丨开源项目怎么保证代码质量？.mp4

46丨为何需要组织类型的仓库？

47丨创建团队的项目.mp4

48丨怎样选择适合自己团队的工作流？.mp4

49丨如何挑选合适的分支集成策略？.mp4

50丨启用issue跟踪需求和任务.mp4

51丨如何用project管理issue？.mp4

52丨项目内部怎么实施code review？.mp4

53丨团队协作时如何做多分支的集成？.mp4

54丨怎样保证集成的质量？.mp4

55丨怎样把产品包发布到GitHub上？.mp4

56丨怎么给项目增加详细的指导文档？.mp4

