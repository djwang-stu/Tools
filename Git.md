

[TOC]



# 参考资料

[廖海峰学git](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840038939c291467cc7c747b1810aab2fb8863508000)

[git官方汉化版文档](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-Git-%E5%88%AB%E5%90%8D)



# 前言

git的使用我们先从命令行的开始学起，学通透了之后才能理解客户端下的git工具（比如大多数大型IDE如Xcode, Android Studio等都集成到git的功能，也有不依赖于IDE的git客户端smartgit[点击下载](http://www.syntevo.com/smartgit/)）



# the usage of git

## [点击下载git for windows](https://git-for-windows.github.io/)

## 打开git bash，学习windows下的基本操作



- windows下盘符转移(d:表示d盘符)

  ```
   cd d:
  ```

- windows下创建目录 

  ```
  mkdir github
  ```

- windows下目录转移 (github为当前目录下的文件夹)

  ```
  cd github
  ```

- windows下的git bash的常用命令

  ```
  ll   以list列表的形式显示当前目录的所有文件及其属性
  ls   ll的简化版，只显示文件名
  touch filename.md  生成一个空白文件。
  ```

- 先禁止crlf,因为只有windows是crlf，而mac和linux是lf。  (global表示应用于全部此电脑创建的仓库)

  ```
  git config --global core.autocrlf false
  ```



- 当前目录为github,在此处创建一个本地仓库

  ```
  git init
  ```

- 编写一个文本文件，但注意不要用windows自带的记事本编辑任何文本文件，否则会遇到不可思议的问题，具体原因不解释。建议notepad++替代记事本，并且把notepad++的默认编码设置为UTF-8 without BOM。此处我创建的是markdown文件 "the usage of git.md"

  ​

- 把文件添加到仓库

  ```
  git add "the usage of git.md"
  ```

- 告诉git，把文件提交到仓库

  ```
   git commit -m "message:I worte the usage of git.md"
  ```

  ​


## git和github的关联

> - git为分布式版本控制系统。同一个git仓库，可以分布到不同的机器上。只要有一台机器上有一个原始版本库，此后其他机器就可以“克隆”这个原始版本库，而且每台机器的版本库是不分主次的。
> - 找一台电脑充当服务器的角色。完全可以自己搭建一台运行git的服务器，但目前无必要。而github就是提供git仓库托管服务的，可以免费获得git远程仓库

本地git仓库和github仓库之间的传输是通过SSH加密的，所以需要一点设置。

1.  创建ssh key，在git bash中

    ```
    ssh-keygen -t rsa -C "youremail@example.com"
    ```

2.  在**用户主目录**(例如C:\Users\djwang\\.ssh\id_rsa)中找到.ssh目录。里面有id_rsa和id_rsa.pub。这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

3.  在github中add ssh key（setting->SSH and GPG keys）。填上任意title，在key文本框里粘贴id_rsa.pub文件的内容。**（id_rsa.pub文件用记事本打开）**

4.  在github中创建一个repo。repo的名字为github

5.  把一个已有的本地仓库与github库关联，然后把本地仓库的内容推送到github仓库

        ​```
        git remote add origin git@github.com:xianliti/github.git
        ​```

    > 远程库的名字为origin，当然可以修改为其他名字，但是origin这个名字一看就知道是远程库（git的默认叫法）



6.  把本地库的内容推送到远程库。第一次使用git的clone或者push命令连接github时会得到的一个SSH警告,忽视即可。

    ```
    git push -u origin master
    ```

    由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

    从现在起，只要本地做了提交，就可以通过命令

    ```
    git push origin master
    ```

    SSH警告

    ```github
    $ git push -u origin_name master
    The authenticity of host 'github.com (192.30.253.112)' can't be established.
    RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added 'github.com,192.30.253.112' (RSA) to the list of known hosts.
    Counting objects: 24, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (15/15), done.
    Writing objects: 100% (24/24), 4.11 KiB | 0 bytes/s, done.
    Total 24 (delta 5), reused 0 (delta 0)
    remote: Resolving deltas: 100% (5/5), done.
    To github.com:xianliti/github.git
    * [new branch]      master -> master
    Branch master set up to track remote branch master from origin_name.
    ```
   > 解读：这是第一次使用git的clone或者push命令连接github时会得到的一个警告。需要你确认github的key的指纹信息是否真的来自github的服务器，输入yes回车即可。最后git会输出一个警告，告诉你已经把github的key添加到本机的一个信任列表中了。

# git 基础

## 获取git仓库

> 如下有三个方法，严格而言，只有方法1,2称为生成git仓库。方法3实际上是本地仓库与远程仓库的关联。

1. 在现有项目或目录下导入所有文件到git中到创建一个本地仓库,实现对这个目录下所有文件的版本管理

   ```
   git init
   ```

2. 从一个服务器克隆一个现有的远程仓库

   ```
   git clone [url/ssh]
   例如
   git clone git@github.com:xianliti/tools
   ```

3. 把一个**已有的本地仓库**与**远程仓库(地址用url/ssh表示)**关联，然后把本地仓库的内容推送(pull)到远程仓库 / 把远程仓库的内容抓取(fetch)到本地仓库 

   ```
   git remote add [name:origin] [url/ssh]
   例如
   git remote add origin git@github.com:xianliti/tools
   git remote add my_origin_name https://github.com/xianliti/tools
   <如果不支持https就使用ssh>
   ```


   > GitHub给出的地址不止一个，还可以用`https://github.com/michaelliao/gitskills.git`这样的地址。实际上，Git支持多种协议，默认的`git://`使用ssh，但也可以使用`https`等其他协议。
   >
   > 使用`https`除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用`ssh`协议而只能用`https`。


## 查看提交历史: git log

[参考地址](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%9F%A5%E7%9C%8B%E6%8F%90%E4%BA%A4%E5%8E%86%E5%8F%B2)

下面介绍常用参数

1. -p 显示每次提交的内容差异。也可以加上-2 来仅显示最近两次提交。除了显示基本信息之外，还附带了每次commit的变化。
2. --stat 查看每次提交的简略的统计信息。在每次提交的下面列出所有被修改的文件，有多少文件被修改了以及被谁修改过的文件的那些行被移除或是被添加了。
3. --pretty= 这个选项可以指定使用不同于默认格式的方式展示提交历史，有一些内建的子选项供你选择，比如oneline, short, full, fuller, format展示的信息或多或少有些不同。最有趣的是format，可以定制要显示的记录格式，常用格式见本节参考网页。
4. --since= 或者--until=或者--after=。支持多种格式：比如"2016-12-29"或者"2 years 1 day 3 minutes ago"
5. --autor= 查看指定作者的提交
6. --grep= 搜索提交说明中的关键字



## 撤销操作

[参考网址](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C)

> 接下来会讲解几个撤销操作。注意：有些撤销操作是不可逆的。

1. --amend。==提交信息写错了==，用带此选项的提交命令重新提交。之后它会启动文本编辑器，修改里面的提交信息即可。==提交完后发现漏掉几个文件没有添加==：git commit -m 'initial commit'   git add forgotten_file    git commit --amend. 此时第二次提交将替代第一次提交的结果

2. 取消暂存的文件。(修改后add但未commit)  

   ```
   git reset HEAD filename
   ```

   ​

3. 撤销对文件的修改(修改后未add) 

   ```
   git checkout [filename]
   ```

   > git checkout filename很危险，这意味着你对这个文件做的任何修改都会消失，你只是拷贝了另一个文件来覆盖它。



## 远程仓库的使用

[参考网址](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%BF%9C%E7%A8%8B%E4%BB%93%E5%BA%93%E7%9A%84%E4%BD%BF%E7%94%A8)

> 远程仓库是指托管在因特网或其他网络中的你的项目的版本库。 你可以有好几个远程仓库，通常有些仓库对你只读，有些则可以读写。
>
> 与他人协作涉及管理远程仓库以及根据需要推送或拉取数据。
>
> 管理远程仓库包括了解如何添加远程仓库、移除无效的远程仓库、管理不同的远程分支并定义它们是否被跟踪等等。

### 查看远程仓库

```
git remote -v
```

如果想查看你已经配置的远程仓库服务器，可以运行 `git remote` 命令。 它会列出你指定的每一个远程服务器的简写。 如果你已经克隆了自己的仓库，那么至少应该能看到 origin - 这是 Git 给你克隆的仓库服务器的默认名字：

你也可以指定选项 `-v`，会显示需要读写远程仓库使用的 Git 保存的简写与其对应的 URL。

### 添加远程仓库

```
git remote add <remote-name> <url/ssh>
```

> clone 下来的远程仓库的remote-name默认为origin

### 从远程仓库中抓取（fetch）与拉取（pull）

```
git fetch [remote-name]
fetch命令会访问远程仓库，从中拉取所有你还没有的数据。执行完成后，你将拥有这个远程仓库中所有分支的引用，并且可以随时合并并查看。注意的是它并不会自动合并或修改你当前的工作，当准备好时你必须手动将其合并入你的工作

git pull
如果你有一个分支设置为追踪一个远程分支，可以使用git pull命令来自动抓取并合并远程分支到当前分支，这个操作可能对你来说更舒服。
默认情况下，git clone命令会自动设置本地master分支跟踪克隆的远程仓库的master分支（或不管时什么名字的默认分支），运行git pull通常会从最初克隆的服务器上抓取数据并自动尝试合并到当前所在的分支
```

### 推送到远程仓库(push)

```
git push [remote-name] [branch-name]
当你想要将 master 分支推送到 origin 服务器时（再次说明，克隆时通常会自动帮你设置好那两个名字），那么运行这个命令就可以将你所做的备份到服务器：
只有当你有所克隆服务器的写入权限，并且之前没有人推送过时，这条命令才能生效。 当你和其他人在同一时间克隆，他们先推送到上游然后你再推送到上游，你的推送就会毫无疑问地被拒绝。你必须先将他们的工作拉取下来并将其合并进你的工作后才能推送git pull
```

### 查看远程仓库

```
git remote show [remote-name]
```

> 它同样会列出远程仓库的 URL 与跟踪分支的信息。 这些信息非常有用，它告诉你正处于 master 分支，并且如果运行 git pull，就会抓取所有的远程引用，然后将远程 master 分支合并到本地 master 分支。 它也会列出拉取到的所有远程引用。
### 远程仓库的重命名与移除

```
git remote rename name_from name_to
注意：这同样也会修改你的远程分支名字。过去引用name_from/master，现在引用name_to/master
```

```
git remote rm remote_name
如果因为一些原因想要移除一个远程仓库--你已经从服务器上搬走了或不再想使用某一个特定的镜像了，又或者某一个贡献者不再贡献了.
```



## 打标签(tag)

[参考网站](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE)



## git别名

[参考网站](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-Git-%E5%88%AB%E5%90%8D)



# git分支

[廖海峰git](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001375840038939c291467cc7c747b1810aab2fb8863508000)

[参考资料](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%AE%80%E4%BB%8B)















# 其他


### 常用命令

- git status命令让我们时刻掌握仓库当前的状态
- git diff 查看仓库具体被修改了什么内容
- git log 显示从最近到最远的提交日志。如果输出信息太多，可以加上--pretty=oneline参数，此时看到左边为commit id,右边为提交日志。

> git用HEAD表示当前目录，上一个版本就是HEAD^,上上一个版本就是HEAD^^。或者用HEAD~100表示往上100个版本。

#### 版本回退功能

- git reset --hard  HEAD^    回退到上一个版本，会把被取消的版本从时间线上抹除，即git log不能显示。

- git reset --hard commit_id 回退到任意版本，只要你记得commit_id。

- 想恢复到新版本，但是又不记得commit_id。可以用一下方法找到commit_id。

  git reflog 查看命令历史，以便确定要回到未来的哪个版本。

  ​

#### 重要概念：**工作区和暂存区**

- 工作区working directory。本例中为github

- 版本库repository。工作区有一个隐藏目录.git。这个不算工作区，而是git的版本库

  > 版本库里存了很多东西，其中最重要的就是称为stage(或者叫index)的暂存区，还有git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

  - git add把文件添加进去，实际上就是把文件添加到暂存区
  - git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支

#### 管理修改

> git比其他版本控制系统设计的优越之处在于他跟踪并管理的是修改，而非文件。

- 因此，每次修改，如果不add到暂存区，那就不会加入到commit中



#### 撤销修改

- git checkout --file 可以丢弃工作区的修改
  - file自修改后还没有被放到暂存区（或者删除），撤销修改就回到和版本库一模一样的状态
  - file已经添加到暂存区后又做了修改，现在撤销修改就回到添加到暂存区后的状态
- git reset HEAD file 可以把暂存区的修改撤销掉(unstage)，重新放回工作区
  - file被添加到暂存区，现在撤销修改可以把暂存区的修改回退到工作区。HEAD表示最新的版本
  - 注意到git reset既可以回退版本，又可以把暂存区的修改回退到工作区。

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)一节，不过前提是没有推送到远程库。



#### 删除文件

> 在git中，删除也是一个修改操作。

场景：直接在文件管理器中把没用的文件删除了，这时git知道你删除了文件，工作区和版本库就不一致，用git status可以得知那些文件被删除。

- 选择1：确实要从版本库中删除该文件）git rm filename（这个rm操作是发生在暂存区的）   git commit （把暂存区的内容提交到主分支）
- 选择2：删错了，因为版本库中还有，所以可以恢复到最新版本。 git checkout -- filename

1. 把文件从版本管理中移除并从磁盘中删除 git rm (-f) filename

2. 把文件从版本管理中移除但在磁盘中保留 git rm --cached file.

   staged 和cached是同义词


1. git diff 查看未暂存起来的变化
2. git diff --staged查看已经暂存起来的变化

### 移动文件（重命名）

> git不显式跟踪文件移动操作，如果在git中重命名了某个文件，仓库中存储的元数据并不会体现出这是一次改名操作。

```
git mv file_from file_to
等价于下面三条命令
mv file_from file_to
git rm file_from
git add file_to
```







