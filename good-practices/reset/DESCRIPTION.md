人非圣贤, 孰能无过? 版本控制的很大一个用处就是: 在你 (或者你的队友) 犯错时, 帮助你的项目回到正确的状态.

在这节课程中, 你将学习使用 `git reset` 和 `git revert` 来撤销错误的提交.

---

# Git Reset 的使用方法

让我们回忆一下 Git 的三大区域:

- 工作区 (Working Directory): 你正在编辑的文件所在的地方, 就是你的文件系统管理的目录.
- 暂存区 (Staging Area): 你准备提交的文件所在区域, 这是 Git 管理的.
- 本地仓库 (Local Repository): 你本地的 Git 仓库, 存储所有的提交历史. 其中 HEAD 指向当前分支的最新提交.

`git reset` 的操作, 就是基于之前的历史记录调整这些区域的信息.

---

`git reset` 有三个常用的模式: `--soft`, `--mixed` (默认), 和 `--hard`. 它们的共同特点是接受一个 `commit` 作为参数, 并将当前分支的 HEAD 指向该 `commit`. 比如:

```
git reset d1977cfba62fadd89e2f2f292256866d4da286a5
git reset HEAD (回退到 HEAD 自生, 也就是当前 commit)
git reset HEAD~1 (回退到 HEAD 的上一个提交, 也就是倒数第二个 commit)
```

其中, 参数的缺省值是 HEAD, 也就是默认对于 HEAD 指针不改变.

三种模式的区别在于它们对暂存区和工作区的影响.

---

### Soft 模式

`--soft` 是 "温柔的" reset 模式. 它只会改变 HEAD 指针, 而对于暂存区和工作区都不做任何修改. 也就是说, 你回退到某个 commit 后, 该 commit 之后的所有更改都会被保留在暂存区和工作区中.

一个常见的用例是当你发现自己误打了 commit, 于是想回到 "执行 commit 之前一瞬间" 的状态, 你就可以使用:

```
git reset --soft HEAD~1
```

这会将 HEAD 回退一个 commit, 然后之后的所有操作都会被保留下来移动到暂存区 (因为你 commit 的是暂存区的内容). 你当前工作区的操作也不会被抹除.

---

### Mixed 模式

`--mixed` 是 `git reset` 的默认模式. 它会改变 HEAD 指针, 并且将暂存区的内容重置为指定 commit 的状态, 但是不会修改工作区. 也就是说, 你回退到某个 commit 后, 该 commit 之后的所有更改会被保留在工作区中, 但是不再保留在暂存区.

如果你执行了

```
git reset HEAD~1
```

那么你也会回退到上一个 commit, 但是该 commit 之后的更改会被保留在工作区中, 不再存储在暂存区.

利用这个性质, 我们可以使用这个模式来 "unstage" 一些或全部文件:

```
git reset    # 相当于 git reset --mixed HEAD: 将暂存区所有文件都会移到工作区
git reset file1 file2  # 只将指定的文件从暂存区移到工作区
```

---

### Hard 模式

`--hard` 是 "强硬的" reset 模式. 它会改变 HEAD 指针, 并且将暂存区和工作区都重置为指定 commit 的状态. 也就是说, 你回退到某个 commit 后, 该 commit 之后的所有更改都会被抹除, 无论是在暂存区还是工作区.

⚠️ **警告**: 使用 `--hard` 模式会丢失所有未提交的更改, 包括工作区和暂存区的更改, 并且无法恢复. 请谨慎使用.

通常, 如果你想丢弃你从上一个 commit 以来你在工作区和暂存区的所有更改, 你可以使用:

```
git reset --hard HEAD
```

如果你想不保留痕迹地回到某个 commit, 你可以使用:

```
git reset --hard <commit-hash>
```

---

## Git Revert: 以进为退的安全手段

在单人项目中, `git reset` 是一个非常有用的工具, 但是在多人协作的项目中, 它可能会引起混乱. 因为 `git reset` 会改变提交历史, 这会导致其他协作者的仓库与远程仓库不一致.

> 例如, 如果你做了 `git reset --hard HEAD~1`, 你将不能将这个操作 push 到 remote 仓库. 如果你强制使用 `git push --force` 这么做, 就会导致其他协作者的仓库出现问题.

为了避免这种情况, 我们可以使用 `git revert` 来撤销错误的提交. `git revert` 不会改变提交历史, 而是创建一个新的 commit 来撤销指定的 commit. 这样, 其他协作者的仓库不会受到影响.

`git revert` 同样接受一个参数 `<commit>`, 用来指示要撤销到的 commit, 使用方法和 `git reset` 类似:

```
git revert <commit-hash>
git revert HEAD~1
```

---

## 任务卡

我们在你的 `/home` 目录下创建了一个 `git-reset` 仓库, 请你完成以下任务:

1. 回退到倒数第二个 commit 的状态, 但请不要清空该状态之后的更改. 我们把这个 commit 记为 `x`;
2. 新建一个 commit, 消息任意: 提交在 `x` 之后对于文件 `file1` 的更改, 并丢弃对于其他文件的更改.
3. 运行 `/challenge/submit` 来获取 `/flag`.
