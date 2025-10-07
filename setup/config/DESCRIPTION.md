在这个教程中我假定你已经安装好了 Git。如果你没有安装，我推荐 Windows 用户在 WSL 中安装（以避免经典的CRLF 和 LF 换行符问题），使用你们在上一个 Shell 教程中学到的 `sudo apt install git`。如果是 Mac 用户，可以先安装 Homebrew 然后使用 `brew install git`。

现在，它的目的主要是来解决你们课上在运行 `git commit -m` 时它报的错误，你在当时可能看到它是这样说的

```bash
Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.
```

显然，对于一些学习能力强的人来说他们看到报错可能已经去问过AI来解决问题了，不过我在这里还是想再讲一下：它到底干了什么，然后顺便再提一些 `git` 中别的配置。

---

在这里，我想强调的是，Git 的配置是非常重要的，尤其是用户信息的配置。通过 `git config` 命令，你可以设置许多选项，包括用户的姓名和电子邮件地址。这些信息将会被 Git 用来标识每个提交的作者。

例如，运行我课上讲的 `git log` 命令，你可能会看到如下类似的东西

```bash
commit 9fceb02c0ee4b1a5c0e4b1a5c0ee4b1a5c0ee4b1a5
Author: Your Name <you@example.com>
Date:   Mon Sep 28 12:00:00 2021 +0800

    Your commit message
```

这里的 `Author` 字段就是从你通过 `git config` 设置的信息中获取的。如果你没有正确配置这些信息，Git 将无法识别你的身份，这可能会导致提交记录中缺少作者信息，影响团队协作和代码追踪。怎么配置？很简单，Git 在上面都教你了

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

`--global` 选项表示这些配置将应用于你系统上的所有 Git 仓库。如果你想为某个特定的仓库设置不同的用户信息，可以在该仓库目录下运行相同的命令，但不加 `--global` 选项。**记得一定不要粘贴上面的命令中的 `Your Name` 和 `you@example.com`，而是要替换成你自己的信息。**

---

除了用户信息，`git config` 还允许你设置其他许多选项。例如，你可以配置 Git 的颜色输出，使其在终端中更易读

```bash
git config --global color.ui auto
```

此外，Git 还支持配置别名，还记得我之前教的 Bash 别名吗？Git 也有类似的功能。刘祎禹学长在[他的博客](https://lau.yeeyu.org/blog-zh-cn/git-usage-misc-zh-cn/)中提到了一些有用的 Git 别名，例如

- `unstage`：相当于 `git reset HEAD --`，用于取消暂存区的更改

    ```bash
    git config --global alias.unstage 'reset HEAD --'
    ```

- `full-pull`：相当于 `git pull --recurse-submodules`，用于拉取包含子模块的仓库

    ```bash
    git config --global alias.full-pull 'pull --recurse-submodules'
    ```

... 诸如此类的别名可以极大地提高你的工作效率，建议根据自己的习惯进行配置。

最后，所有这些配置都会被存储在一个名为 `.gitconfig` 的文件中，位于你的用户主目录下。你可以直接编辑这个文件来查看或修改你的配置。

你可以使用以下命令来查看当前的 Git 配置

```bash
git config --list
```
这将显示所有当前的配置选项及其值。如果你只配置了用户名和邮箱地址，你应该会看到类似如下的输出

```bash
[user]
    name = Your Name
    email = you@example.com
```

本章不设置挑战。作为阅读章节即可。如果你真能通过某些手段在本关正确拿到 flag 并提交，**第一位正确的提交者**将会获得一杯奶茶的奖励。