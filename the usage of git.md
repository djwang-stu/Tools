# the usage of git

## 下载git for windows

## 打开git bash



- windows下盘符转移 cd d:

- windows下创建目录 mkdir github

- windows下目录转移 cd github

- 先禁止crlf,因为只有windows是crlf，而mac和linux是lf。

  git config --global core.autocrlf false  (global表示应用于全部此电脑创建的仓库)

- 当前目录为github,在此处创建一个本地仓库

  git init

- 编写一个文本文件，但注意不要用windows自带的记事本编辑任何文本文件，否则会遇到不可思议的问题，具体原因不解释。建议notepad++替代记事本，并且把notepad++的默认编码设置为UTF-8 without BOM。此处我创建的是markdown文件 "the usage of git.md"

- 把文件添加到仓库

  git add "the usage of git.md"

- 告诉git，把文件提交到仓库

  1. 添加本次提交说明： git commit -m "I worte the usage of git"
  2. 或者不带提交说明，但不建议 git commit



### 常用命令

- git status命令让我们时刻掌握仓库当前的状态
- git diff 查看仓库具体被修改了什么内容
- git log 显示从最近到最远的提交日志。如果输出信息太多，可以加上--pretty=oneline参数，此时看到左边为commit id,右边为提交日志。

> git用HEAD表示当前目录，上一个版本就是HEAD^,上上一个版本就是HEAD^^。或者用HEAD~100表示往上100个版本。

#### 版本回退功能

* git reset --hard  HEAD^    回退到上一个版本，会把被取消的版本从时间线上抹除，即git log不能显示。

* git reset --hard commit_id 回退到任意版本，只要你记得commit_id。

* 想恢复到新版本，但是又不记得commit_id。可以用一下方法找到commit_id。

  git reflog 查看命令历史，以便确定要回到未来的哪个版本。

  ​


#### 重要：**工作区和暂存区**

* 工作区working directory。本例中为github

* 版本库repository。工作区有一个隐藏目录.git。这个不算工作区，而是git的版本库

  > 版本库里存了很多东西，其中最重要的就是称为stage(或者叫index)的暂存区，还有git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

  * git add把文件添加进去，实际上就是把文件添加到暂存区
  * git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支



#### 管理修改

> git比其他版本控制系统设计的优越之处在于他跟踪并管理的是修改，而非文件。

* 因此，每次修改，如果不add到暂存区，那就不会加入到commit中





#### 撤销修改

* git checkout --file 可以丢弃工作区的修改
  * file自修改后还没有被放到暂存区（或者删除），撤销修改就回到和版本库一模一样的状态
  * file已经添加到暂存区后又做了修改，现在撤销修改就回到添加到暂存区后的状态
* git reset HEAD file 可以把暂存区的修改撤销掉(unstage)，重新放回工作区
  * file被添加到暂存区，现在撤销修改可以把暂存区的修改回退到工作区。HEAD表示最新的版本
  * 注意到git reset既可以回退版本，又可以把暂存区的修改回退到工作区。

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)一节，不过前提是没有推送到远程库。



#### 删除文件

> 在git中，删除也是一个修改操作。

场景：直接在文件管理器中把没用的文件删除了，这时git知道你删除了文件，工作区和版本库就不一致，用git status可以得知那些文件被删除。

* 选择1：确实要从版本库中删除该文件）git rm filename（这个rm操作是发生在暂存区的）   git commit （把暂存区的内容提交到主分支）
* 选择2：删错了，因为版本库中还有，所以可以恢复到最新版本。 git checkout -- filename



### git和github的关系

* git为分布式版本控制系统。同一个git仓库，可以分布到不同的机器上。只要有一台机器上有一个原始版本库，此后其他机器就可以“克隆”这个原始版本库，而且每台机器的版本库是不分主次的。
* 找一台电脑充当服务器的角色。完全可以自己搭建一台运行git的服务器，但目前无必要。而github就是提供git仓库托管服务的，可以免费获得git远程仓库

本地git仓库和github仓库之间的传输是通过SSH加密的，所以需要一点设置。

1. 创建ssh key. 在git bash中

   ```
   ssh-keygen -t rsa -C "youremail@example.com"
   ```

2. 在用户主目录中找到.ssh目录。里面有id_rsa和id_rsa.pub。这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

3. 在github中add ssh key。填上任意title，在key文本框里粘贴id_rsa.pub文件的内容。

4. 在github中创建一个repo。repo的名字为github

5. 把一个已有的本地仓库与github库关联，然后把本地仓库的内容推送到github仓库

   ```
   git remote add origin git@github.com:xianliti/github.git
   ```

   远程库的名字为origin，当然可以修改为其他名字，但是origin这个名字一看就知道是远程库（git的默认叫法）

   ​

6. 把本地库的内容推送到远程库

   ```
   git push -u origin master
   ```

   由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

   从现在起，只要本地做了提交，就可以通过命令

   ```
   git push origin master
   ```

   ​

   ​

   SSH警告

   ```
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



