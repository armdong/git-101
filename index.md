# The Basics for Git and Github

## Git 初始设置

- **配置用户信息**

  > 初次使用Git前应该要设置你的用户名和邮件地址。
  ```
  $ git config --global user.name "your name"
  $ git config --global user.email "email@example.com"
  ```

- **配置文本编辑器**

  > 当 Git 需要你输入信息时会调用文本编辑器，Git 会使用操作系统默认的文本编辑器，通常是 Vim。
  > 如果你想使用自定义的文本编辑器，可以这样做：
  ```
  $ git config --global core.editor atom
  ```
  > 这样，就设置了 Atom 为你的默认文本编辑器了。

- **检查配置信息**

  > 如果想要检查你的 Git 配置，可以使用 `git config --list` 命令来列出所有 Git 当前的配置项。
  ```
  $ git config --list
  core.symlinks=false
  core.autocrlf=true
  core.fscache=true
  color.diff=auto
  color.status=auto
  color.branch=auto
  color.interactive=true
  user.name=your name
  user.email=email@example.com
  core.editor=atom
  ...
  ```
  > 你如果想查看某一特定项的配置信息，你可以通过输入 `git config <key>` 来查看。
  ```
  $ git config user.email
  email@example.com
  ```

## Git 基础

### 获取 Git 仓库

+ **在现有目录中初始化仓库**

  > 如果你打算使用 Git 对现有的项目进行管理，你只需要进入该项目目录并输入：
  ```
  $ git init
  ```
  > 该命令将创建一个名为 .git 的子目录，这个子目录包含你初始化的 Git 仓库中所有的必须文件。
  > 该命令仅仅是做了一个初始化操作，项目中的文件还并没有被跟踪。
  > 你可以通过 `git add` 命令来实现对指定文件的跟踪，然后执行 `git commit` 命令提交：
  ```
  $ git add <file name>
  $ git add index.md
  $ git commit -m 'added index.md file to this repository'
  ```

+ **克隆现有的仓库**

### 记录每次更新到仓库

### 查看提交历史

### 撤消操作

### 远程仓库的使用

### 打标签

### Git 别名
