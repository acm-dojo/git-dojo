在上一章节的 “Branch” 里，我们学习了如何创建和切换分支，以及如何合并分支。不知道各位还是否记得，合并分支可能会遇到冲突（conflicts）？如果你同时在两个分支上修改了同一份代码（这在多人合作中事实上很常见！），那么到底是保留你的更改，还是保留另外一个人的更改？这时候需要你手动解决冲突。

## 什么是合并冲突？

Git 足够智能，可以自动合并很多情况（比如你在文件 A 的第 10 行做了修改，而另一个分支在文件 B 的第 50 行做了修改）。但当两个分支都对文件 A 的第 10 行进行修改时，Git 不知道该听谁的，它就会停下来，把决定权交给你。

当 Git 无法自动合并两个分支的更改时，就会发生合并冲突。这通常发生在：
- 同上面所说，两个分支修改了同一个文件的同一行
- 一个分支删除了文件，而另一个分支修改了该文件

## 识别冲突

当发生冲突时，Git 会在文件中插入冲突标记：

```
<<<<<<< HEAD
你当前分支的代码
=======
另一个分支的代码
>>>>>>> branch-name
```

事实上，冲突解决并不复杂，各位应该对它祛魅，解决过一次就会发现它其实并没有那么可怕。

各位可以在自己的终端里面随便新建一个文件夹试一试，我把命令贴在下面，逐行运行，你们现在应该已经能看懂这些命令了：

```bash
mkdir conflict-demo && cd conflict-demo

git init

echo "version=1" > app.txt

git add . && git commit -m "init"

# 在 test 分支修改同一行
git switch -c test

echo "version=2-from-test" > app.txt

git commit -am "test: update version"

# 回到 main，做不同修改
git switch main

echo "version=2-from-main" > app.txt

git commit -am "main: update version"

# 合并产生冲突
git merge test
```

你们应该会看到类似下面的输出：

```
Auto-merging app.txt
CONFLICT (content): Merge conflict in app.txt
Automatic merge failed; fix conflicts and then commit the result.
```

当你打开 `app.txt` 文件时，你会看到：

```
<<<<<<< HEAD
version=2-from-main
=======
version=2-from-test
>>>>>>> test
```

## 解决冲突的步骤

1. 查看冲突文件
    ```bash
    git status
    ```

2. 编辑冲突文件
    - 删除冲突标记（`<<<<<<<`, `=======`, `>>>>>>>`）
    - 保留你想要的代码
    - 或者合并两个版本的代码

3. 标记冲突已解决
    ```bash
    git add <文件名>
    ```

4. 完成合并
    ```bash
    git commit
    ```

>   还有一些其他「小技巧」：
>
>   「走为上计」：如果你觉得冲突太复杂，想要放弃合并，可以使用 `git merge --abort` 来取消合并操作，回到合并前的状态。
>
>   「言听计从」：如果你决定保留别人的更改，可以使用 `git merge -X theirs ...`；这里 `-X theirs` 表示在冲突时倾向于对方分支的改动，`...` 是你要合并的分支名。
>
>   「固执己见」：如果你决定保留自己的更改，可以使用 `git merge -s ours ...`；这会记录一次合并但保留当前分支的内容，务必谨慎使用。
>    
>    以上内容来源于 [刘祎禹学长的博客](https://lau.yeeyu.org/blog-zh-cn/git-usage-merging-zh-cn/)，他取的这三个名字实在是太好了，所以我也搬过来了🤣。

## RECAP

在本章中，你学习了如何识别并解决合并冲突，让两条时间线重新汇合。

### 核心概念

- 当 Git 无法自动决定同一位置的最终内容时，它会请求你介入。
- **冲突标记**：`<<<<<<<`、`=======`、`>>>>>>>` 展示当前分支与目标分支的差异。
- 遇到冲突不要慌张：检查文件、删除标记、保留正确内容、重新提交。
- 必要时可以中止合并，或使用 ours/theirs 等策略快速决策。

### 命令速查表

- `git status`：在有冲突时，可以列出冲突文件清单
- `git diff --merge`：查看冲突双方的差异
- `git merge --abort`：出现混乱时快速撤退 🏳️

### 一些 Tips

- 打开冲突文件时先读懂标记，明确哪部分来自 `HEAD`、哪部分来自对方。
- 完成编辑后务必删除所有冲突标记，避免把 `<<<<<<<` 之类提交进历史。
- 记得提交你已经解决冲突后的文件哦！并且，提交前可以再次运行 `git status`，确认没有未解决的冲突或遗留文件。

---

> 以下内容不需要掌握，作为阅读材料即可。

你们在合并两个分支时，你还有可能看到 Git 如下的报错，然后说什么 `--ff-only`, `--no-ff`，`--squash` 之类的选项。别慌，以防你碰巧碰到了它们，我在这里也解释一下。你们可能看到这样的东西：

```bash
$ git pull
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:
hint:   git config pull.rebase false  # merge (the default strategy)
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
fatal: Need to specify how to reconcile divergent branches.
```

这个提示会在以下情况出现：

- 你本地的当前分支（比如 main）有了一些新的提交。

- 与此同时，远程仓库的同一个分支 (origin/main) 也有了别人推送的、你本地没有的新提交。

- 这时，你的本地分支和远程分支就“分叉（Diverged）”了。

Git 上面提到的 `--ff-only`, `--no-ff`，`--squash` 是“合并策略”。这些策略决定的是历史记录的结构，而不是代码内容的合并方式。代码内容的合并方式就是我们讲的那些东西。

- fast-forward：历史线性，但看不见合并点。
- --no-ff：保留合并节点，便于回溯特性分支。
- squash merge：把分支压成一次提交，整洁但丢失中间历史。
- rebase vs merge：
    - rebase：历史更线性；不要对已共享分支重写历史。
    - merge：保留自然历史；可能更“分叉”，但安全。

---

## 任务卡

我们已经在 `~/dojo-conflict` 中准备了一份“正在撰写的小说”。`main` 分支和 `feature/story` 分支分别对第三章做了不同修改。当你尝试把特性分支合并回 `main` 时，一定会遇到冲突。

请进入练习仓库：`cd ~/dojo-conflict`，执行 `git merge feature/story`，观察 Git 报出的冲突信息。

打开 `story.txt`，消除冲突标记，把内容整理为：
    ```
    Chapter 1: Arrival
    Chapter 2: Tension builds
    Chapter 3: Main timeline update.
    Chapter 3 (feature): Alternate timeline reveal.
    Chapter 4: Cliffhanger
    ```

使用 `git add story.txt` 标记冲突已解决，并通过 `git commit` 创建合并提交（默认的 Merge 信息即可）。

确认工作区干净、没有残留的冲突标记后，运行 `/challenge/submit` 验证结果。
