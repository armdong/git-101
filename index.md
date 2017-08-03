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
