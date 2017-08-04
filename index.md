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

- **在现有目录中初始化仓库**

  > 如果你打算使用 Git 对现有的项目进行管理，你只需要进入该项目目录并输入：
  ```
  $ git init
  ```
  > 该命令将创建一个名为 .git 的子目录，这个子目录包含你初始化的 Git 仓库中所有的必须文件。
  > 该命令仅仅是做了一个初始化操作，项目中的文件还并没有被跟踪。
  > 你可以通过 `git add` 命令来实现对指定文件的跟踪，然后执行 `git commit` 命令提交：
  ```
  $ git add index.md
  $ git commit -m 'added index.md file to this repository'
  ```

- **克隆现有的仓库**

  > 如果你想获得一份已经存在的 Git 仓库的拷贝，就需要用到 `git clone` 命令。
  > 克隆仓库的命令格式是 `git clone [url]`。比如，要克隆 jQuery 库，可以用下面的命令：
  ```
  $ git clone git@github.com:jquery/jquery.git
  ```
  > 这个命令执行之后，会在当前目录下创建一个名为 "jquery" 的目录，并在这个目录下初始化一个 `.git` 文件夹，从远程仓库拉取下所有数据放入 `.git` 文件夹，然后从中读取最新版本的文件的拷贝。
  > 如果你想在克隆远程仓库的时候，自定义本地仓库的名字，你可以使用如下命令：
  ```
  $ git clone git@github.com:jquery/jquery.git my-jquery
  ```
  > 这将执行与上一个命令相同的操作，不过在本地创建的仓库名字变为 `my-jquery`。

### 记录每次更新到仓库

- **检查当前文件状态**

  > 要查看哪些文件处于什么状态，可以用 `git status` 命令。
  ```
  $ git status
  ```

- **跟踪新文件**

  > 使用命令 `git add <filename>` 开始跟踪一个文件。
  ```
  $ git add index.md
  ```
  > 或者使用 `git add .` 命令跟踪所有新增文件。
  ```
  $ git add .
  ```

- **暂存已修改文件**

  > 如果一个文件已经被跟踪，如果再对这个文件进行修改，可以使用 `git add` 命令暂存已修改的文件。
  ```
  git add README.md
  ```

- **状态简览**

  > `git status` 命令的输出十分详细，但内容比较多。如果你使用 `git status -s` 命令或者 `git status --short` 命令，你将得到一种更为紧凑的格式输出。
  ```
  $ git status -s
  M  README.md
   M .gitignore
  MM Rakefile
  A  lib/git.rb
  ?? LICENSE.md
  ```
  > 新添加的未跟踪文件前面有 ?? 标记，新添加到暂存区中的文件前面有 A 标记，修改过的文件前面有 M 标记。 你可能注意到了 M 有两个可以出现的位置，出现在右边的 M 表示该文件被修改了但是还没放入暂存区，出现在靠左边的 M 表示该文件被修改了并放入了暂存区。

- **忽略文件**

  > 一般项目中有些文件我们不想纳入 Git 的管理，也不希望它们出现在未跟踪的文件列表中。在这种情况下，我们可以在项目根目录创建一个名为 `.gitignore` 的文件，列出要忽略的文件。
  ```
  $ cat .gitignore
  node_modules/
  /*.log
  .DS_Store
  ...
  ```
  > 文件 `.gitignore` 的格式规范如下：
    + 所有空行或者以 ＃ 开头的行都会被 Git 忽略。
    + 可以使用标准的 glob 模式匹配。
    + 匹配模式可以以（/）开头防止递归。
    + 匹配模式可以以（/）结尾指定目录。
    + 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。

- **查看已暂存和未暂存的修改**

  > 如果 `git status` 命令的输出对于你来说过于模糊，你想知道具体修改了什么地方，可以用 `git diff` 命令。

  > 查看尚未暂存的文件更新了哪些部分，不加参数直接输入 `git diff`。

  > 若要查看已暂存的将要添加到下次提交里的内容，可以用 `git diff --cached` 命令。（Git 1.6.1 及更高版本还允许使用 `git diff --staged`，效果是相同的，但更好记些。）

- **提交更新**

  > 当所有的新增文件和已修改的文件都放到暂存区后，我们可以利用 `git commit` 命令提交到本地仓库。提交之前一般要运行 `git status` 查看下当前所有文件状态是否都已经被放到暂存区。
  ```
  $ git commit
  ```
  > 这种方式会启动文本编辑器输入本次提交的说明。 (默认会启用 shell 的环境变量 $EDITOR 所指定的软件，一般都是 vim 或 emacs。当然也可以使用 git config --global core.editor 命令设定你喜欢的编辑软件。）

  > 另外，你也可以在 `commit` 命令后添加 `-m` 选项，将提交信息与命令放在同一行，如下所示：
  ```
  $ git commit -m "added some adjust"
  ```
  
- **跳过使用暂存区域**



- **移除文件**



- **移动文件**



### 查看提交历史

### 撤消操作

### 远程仓库的使用

### 打标签

### Git 别名
