在使用 Git 进行多人合作的时候, 许多时候我们需要将自己的进度和他人共享, 或者获取他人的新进展. 这时候, 我们就需要使用 `git fetch` 和 `git pull` 等命令来实现本地仓库与远程仓库的同步.

---

`git fetch` 命令用于从远程仓库获取最新的更新. 它会将远程仓库的数据下载到你的本地, 但**不会**自动合并或修改你当前的工作. 

```bash
# 从名为 origin 的远程仓库获取更新
$ git fetch origin
```

如果命令行没有任何输出, 说明你的本地仓库已经是最新的. 否则, 你可能会看到类似下面的输出:

```bash
From https://github.com/acm-dojo/sudo
    44bc5d6..3737415  main       -> origin/main
```

这表示远程仓库 `origin` 的 `main` 分支有了新的提交. `origin/main` 是一个远程跟踪分支, 它反映了远程仓库 `main` 分支在你上次 `fetch` 时的状态. 

要将这些获取到的更新合并到你当前的本地分支, 你需要接着运行 `git merge`：

```bash
# 将 origin/main 分支合并到当前分支
git merge origin/main
```

> 在 Git 中, 远程和你的本地的操作都以分支 (branch) 形式存储. 你可以使用 `git merge` 来合并它们. 这在后续的教程中会详细说明.

---

为了简化这个两步过程, Git 提供了 `git pull` 命令. 它相当于 `git fetch` 和 `git merge` 的组合：

```bash
# 等同于 git fetch origin && git merge origin/main
git pull origin main
```

如果你当前的分支已经设置了上游分支 (upstream branch), 你可以省略远程仓库和分支名称, 直接运行 `git pull`.

> 你克隆下的仓库默认会有一个名为 `origin` 的远程仓库, 以及一个名为 `main` 的主分支. 因此, 你可以省略参数, 直接运行 `git pull`.

---

有 `git pull` 获取远程的更新, 当然也就有 `git push` 将你的本地更新推送到远程仓库. 它和 `git pull` 是相反的过程. 

```bash
git push origin main
```

同理, 在有上游分支的情况下, 你也可以省略远程仓库和分支名称.

---

上一个挑战中, 你已经克隆了一个远程仓库. 现在, 这个远程仓库有了新的更新. 你的任务是用将这些更新同步到你的本地仓库.

在更新后的仓库中, `README.md` 文件的内容已经被修改. 请根据它的提示, 完成本次挑战.
