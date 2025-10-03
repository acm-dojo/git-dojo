在讲解了 Git 的基本配置后，我们接下来要讨论的是分支管理。分支是 Git 中一个非常强大的特性，它允许你在不影响主干代码的情况下进行开发。类比的说，如果仓库是“时光机”，那么分支就是“平行宇宙的时间线”。你可以在一个分支上开发新功能，同时主分支保持稳定，等新功能开发完成并经过测试后，再将其合并回主分支。

在 Git 中，创建和管理分支非常简单。你可以使用以下命令来创建一个新分支：

```bash
git branch <branch-name>
```

然后，切换到新分支：

```bash
git checkout <branch-name>
```

有没有“只做一次”的脚本来切换分支呢？有的兄弟，有的：

```bash
git checkout -b <branch-name>
```

这条命令会同时创建并切换到新分支。你可以在新分支上进行开发，提交更改，就像在主分支上一样。所有之前你学到的命令，`git add`、`git commit`、`git status`，都可以在分支上使用。

当你完成了在分支上的开发，并且确认代码没有问题后，你可以将分支合并回主分支。合并回主分支这件事你既可以在本地完成，也可以在远程仓库中通过 Pull Request（PR）来完成。这里我们先介绍本地合并的方式：

```bash
git checkout main  # 切换回主分支
git merge <branch-name>  # 将指定分支合并到主分支
```

有时候，合并分支可能会遇到冲突（conflicts）。如果你同时在两个分支上修改了同一份代码（这在多人合作中事实上很常见！），那么到底是保留你的更改，还是保留另外一个人的更改？这时候需要你手动解决冲突，我们把这个话题留到 "Oh Shit, Git" 模块中详细讲解，毕竟它较为头疼。

我们再来提一嘴分支的命名规范。和 `commit message` 一样，为了让团队协作更加顺畅，建议大家在创建分支时遵循一定的命名规范。例如，可以使用以下格式：

```
feature/<feature-name>  # 新功能
bugfix/<bug-description>  # Bug 修复
hotfix/<hotfix-description>  # 紧急修复
```

我之前还说了 “你可以在 GitHub 上创建 Pull Request（PR）来合并分支”。通过 PR 来合并分支事实上它不止能干“合并”的事，它更重要的作用是一种**协作方式**，它允许你在合并代码之前，先对代码进行审查和讨论。通过 PR，团队成员可以查看你的更改，提出意见，甚至直接在你的分支上进行修改。如果你要贡献代码到一些大项目中，你一般来说只能通过 PR 来贡献代码，因为你没有他们代码库的写入权限。PR 在 Merge 意义上其实 Nothing Special。你在创建 PR 的状态栏上应该能看到类似这样的东西：

![](https://cdn.nodeimage.com/i/mi15aop6o7LEGqVSBGKT9jaEDkayu9Nk.png)

左边是你要合并的分支，右边是目标分支。这与你本地的操作是类似的。

最后，我还要介绍一下 `git stash` 命令。当然，你们现在不用掌握它，不过知道一下总归是好的。当你在运行 `git checkout` 切换分支时，如果工作区有未提交的更改，Git 会阻止你切换分支。这时你可以使用 `git stash` 命令将未提交的更改暂存起来，等切换到目标分支后再恢复。在你们看到这里的时候，大概率助教已经给你们讲了 栈 (Stack) 这个数据结构~~（好吧可能他也只讲了讲STL的栈怎么用吧）~~。事实上，`git stash` 就是利用栈的特性来保存和恢复工作区的状态。具体而言：

```bash
git stash push -m "some unsaved work" # 缓存这些未提交的更改
git checkout some_new_branch # 切换到新分支
...
# 当你新分支上的工作完成后
git checkout previous_branch # 切换回之前的分支
git stash pop # 看！这就是栈！push 进去的东西 pop 出来
```

## RECAP

在本章中，你学习了如何利用分支隔离工作并安全地合并回主干。

### 核心概念

- **分支可以理解成平行时间线**：在不打扰 `main` 的情况下开发新功能或修复问题。
- **分支命名规范**：用 `feature/`、`bugfix/` 等前缀，类似于 commit message 的规范。
- **临时存储工作区**：`git stash` 用栈的方式保存未提交的改动，方便切换分支。

### 关键命令

- `git branch <branch-name>`：创建新分支
- `git checkout <branch-name>`：切换到指定分支
- `git checkout -b <branch-name>`：创建并切换分支
- `git merge <branch-name>`：把目标分支合并进当前分支
- `git stash push -m "<note>"` / `git stash pop`：暂存并恢复未提交更改

### 命令速查表

- `git branch feature/ui`：新建 `feature/ui` 分支
- `git checkout -b feature/ui`：新建并切换到 `feature/ui`
- `git checkout feature/ui`：进入该分支继续开发
- `git checkout main && git merge feature/ui`：返回 `main` 并完成合并
- `git stash push -m "WIP logs"`：保存未完成的工作以便切换
- `git stash list` / `git stash pop`：查看并取回暂存的更改

### 一些 Tips

- 合并前记得回到目标分支（通常是 `main`）。
- 分支上的提交和主分支完全一样，放心使用 `git add` / `git commit`。

---

## 任务卡

现在轮到你来实践一次分支协作流程了！我们已经在 `~/dojo-branch` 中准备好一个仓库，其中 `main` 分支上有一份日常进度日志，但第三天的记录还在草稿状态，且目前保持在未提交的工作区里。

请按照下面的步骤完成练习：

进入目录：`cd ~/dojo-branch`，创建并切换到新分支，名字叫 `feature/progress-log`。

打开 `progress.md`，新增一行 `Day 3: learned branch.`。使用 `git add` 和 `git commit` 提交更改，提交信息为 `branch: ACM Dojo`。

运行 `/challenge/submit` 检查结果。