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



