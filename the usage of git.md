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

    ​