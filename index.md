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

  > 尽管使用暂存区域的方式可以精心准备要提交的细节，但有时候这么做略显繁琐。 Git 提供了一个跳过使用暂存区域的方式， 只要在提交的时候，给 `git commit` 加上 `-a` 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 `git add` 步骤：
  ```
  $ git commit -a -m 'added all files to this repository'
  ```

- **移除文件**

  > 要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说，是从暂存区域移除），然后提交。 可以用 `git rm` 命令完成此项工作，并连带从工作目录中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。

  > 如果只是简单地从工作目录中手工删除文件，运行 `git status` 时就会在 “Changes not staged for commit” 部分（也就是 未暂存清单）看到：
  ```
  $ rm PROJECTS.md
  $ git status
  On branch master
  Your branch is up-to-date with 'origin/master'.
  Changes not staged for commit:
    (use "git add/rm <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

          deleted:    PROJECTS.md

  no changes added to commit (use "git add" and/or "git commit -a")
  ```
  > 然后再运行 `git rm` 记录此次移除文件的操作：
  ```
  $ git rm PROJECTS.md
  rm 'PROJECTS.md'
  $ git status
  On branch master
  Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

      deleted:    PROJECTS.md
  ```
  > 下一次提交时，该文件就不再纳入版本管理了。 如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 `-f`（译注：即 force 的首字母）。 这是一种安全特性，用于防止误删还没有添加到快照的数据，这样的数据不能被 Git 恢复。

  > 另外一种情况是，我们想把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中。 换句话说，你想让文件保留在磁盘，但是并不想让 Git 继续跟踪。 当你忘记添加 `.gitignore` 文件，不小心把一个很大的日志文件或一堆 `.a` 这样的编译生成文件添加到暂存区时，这一做法尤其有用。 为达到这一目的，使用 `--cached` 选项：
  ```
  $ git rm --chached README.md
  ```

  > `git rm` 命令后面可以列出文件或者目录的名字，也可以使用 `glob` 模式。 比方说：
  ```
  $ git rm log/\*.log
  ```
  > 注意到星号 `*` 之前的反斜杠 `\`， 因为 Git 有它自己的文件模式扩展匹配方式，所以我们不用 shell 来帮忙展开。 此命令删除 `log/` 目录下扩展名为 `.log` 的所有文件。 类似的比如：
  ```
  $ git rm \*~
  ```
  > 该命令为删除以 `~` 结尾的所有文件。

- **移动文件**

  > Git 中移动文件可以用这个命令 `git mv <file_from> <file_to>`
  ```
  $ git mv index.js ./src/index.js
  ```


### 查看提交历史

> 如果想查看一个项目的提交历史，可以使用 `git log` 命令进行查看。

> 如果想显示每次提交的内容差异，一个常用的选项是 `-p`，你也可以加上 `-2` 来显示最近两次提交：
  ```
  $ git log -p
  $ git log -p -2
  ```

> 如果你想看到每次提交的简略的统计信息，你可以使用 `--stat` 选项：
  ```
  $ git log --stat
  ```
  > `--stat` 选项在每次提交的下面列出额外的所有被修改的文件、有多少文件被修改了以及被修改过的文件的哪些行被移除或是添加了，每次提交的最后还有一个总结。

> 另外一个常用的选项是 `--pretty`。这个选项可以制定使用不同于默认格式的方式展示提交历史。这个选项有一些内建的子选项可供使用。比如 `oneline` 将每个提交放在一行显示，查看的提交数很大时非常有用。另外还有 `short` , `full` 和 `fuller` 可以用。
  ```
  $ git log --pretty=oneline
  $ git log --pretty=short
  $ git log --pretty=full
  $ git log --pretty=fuller
  ...
  ```

> 其中，最有意思的是 `format`，可以定制要显示的记录格式。这样的输出对后期提取分析格外有用——因为你知道输出的格式不会随着 Git 的更新而发生改变：
  ```
  $ git log --pretty=format:"%h - $an, $ar : $s"
  7f32bb6 - armdong, 3 days ago : 移动文件
  a6105db - armdong, 3 days ago : 移除文件
  129a1fd - armdong, 3 days ago : 跳过使用暂存区域
  d3a5ac8 - armdong, 3 days ago : 提交更新
  2331e2f - armdong, 3 days ago : 查看已暂存和未暂存的修改
  cb0395d - armdong, 3 days ago : 忽略文件
  f5a40db - armdong, 3 days ago : 状态简览调整
  264c059 - armdong, 3 days ago : 状态简览
  ...
  ```

`git log --pretty=format` 常用的选项如下：
 item | description
 :--- | :---
 %H   | 提交对象（commit）的完整哈希字串
 %h   | 提交对象的简短哈希字串
 %T   | 树对象（tree）的完整哈希字串
 %t   | 树对象的简短哈希字串
 %P   | 父对象（parent）的完整哈希字串
 %p   | 父对象的简短哈希字串
 %an  | 作者（author）的名字
 %ae  | 作者的电子邮件地址
 %ad  | 作者修订日期（可以用 --date= 选项定制格式）
 %ar  | 作者修订日期，按多久以前的方式显示
 %cn  | 提交者（committer）的名字
 %ce  | 提交者的电子邮件地址
 %cd  | 提交日期
 %cr  | 提交日期，按多久以前的方式显示
 %s   | 提交说明


### 撤消操作

### 远程仓库的使用

### 打标签

### Git 别名
