你有没有尝试过去部署别人的项目? 开源世界有着相当多优质的项目; 而在本机上使用它们的第一步往往就是使用 `git clone` 命令将它们克隆到本地.

在本挑战中, 我们将学习如何使用 `git clone` 命令来克隆远程仓库.

---

Git clone 的基本语法是 `git clone <repository-url>`, 其中 `<repository-url>` 填写你想要克隆的远程仓库的 URL.

如果你想要克隆的仓库在 GitHub 上, 你可以在该仓库的主页上找到绿色的 "Code" 按钮, 点击它会显示出仓库的 URL. 你可以选择使用 HTTPS 或 SSH 的 URL.

```bash
git clone https://github.com/RayZh-hs/neofrp.git
```

执行上述命令后, 你会在当前目录下看到一个名为 `neofrp` 的文件夹, 里面包含了该仓库的所有内容.

> 如果你想要使用 SSH, 你需要确保你的本地机器已经配置了 SSH key 并将其添加到你的 GitHub 账户中. 如果你不知道怎么做, 可以参阅 [GitHub 的官方文档](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh). **这一块本教程不做要求.**

---

`git clone` 命令提供了一些可选参数. 常用的有:

- `git clone <remote-url> <new_path>` 可以指定克隆到的目录名, 而不是使用默认的仓库名.
- `git clone --recursive` 如果仓库中包含子模块 (git 仓库中的 git 子仓库), 你可以使用这个选项来同时克隆所有子模块.
- `git clone -b <branch-name> <remote-url>` 如果你只想克隆某个特定分支 (branch), 可以使用这个选项. (分支在后面会提到)

---

在这个挑战中, 你需要克隆我们准备的一个远程仓库:

[Git Sample Dojo](https://github.com/acm-dojo/git-sample-repo)

将它克隆在你的主目录 `/home/hacker` 下, 不要重命名, 然后运行 `/challenge/submit` 命令提交你的结果.
