在开始使用 Git 之前，你需要先初始化一个 Git 仓库。

让我们从最基础的命令开始：`git init`！

---

## 什么是 Git 仓库？ 

Git 仓库（repository）是一个包含项目所有文件和版本历史的目录。它就像一个时光机，可以让你：
- 追踪文件的每一次修改
- 回到任何历史版本
- 与其他开发者协作
- 管理不同的开发分支

每个 Git 仓库都有一个隐藏的 `.git` 目录，这里存储着所有的版本信息和配置。还记得吗？你可以用 `ls -la` 来查看隐藏文件。

---

## git init 命令

`git init` 是创建新 Git 仓库的命令。它会在当前目录下创建一个新的 Git 仓库。

### 基本用法

```bash
# 在当前目录初始化 Git 仓库
git init

# 创建新目录并初始化 Git 仓库
git init my-project
```

> **TIP** 运行 `git init` 后，你会看到一条消息："Initialized empty Git repository in /path/to/your/directory/.git/" 不要慌张，这只是告诉你当前目录是空的，并且已经成功初始化了一个 Git 仓库。

---

## 验证仓库初始化

初始化仓库后，让我们验证一下是否成功：

```bash
# 查看隐藏的 .git 目录
ls -la

# 检查 Git 状态
git status
```

`ls -la` 命令会显示所有文件，包括隐藏文件。你应该能看到一个 `.git` 目录。

我们后续会详细介绍 `git status` 命令的输出内容，但现在你只需要知道它可以告诉你当前仓库的状态。在新初始化的仓库中，你会看到类似这样的输出：

```
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

`.git` 目录是 Git 的核心，包含了：
- `HEAD`: 指向当前分支的指针
- `config`: 仓库的配置信息
- `objects/`: 存储所有的 Git 对象（commits, trees, blobs）
- `refs/`: 存储分支和标签的引用

> ⚠️ **警告**: 永远不要手动修改 `.git` 目录中的文件！这可能会损坏你的仓库。

让我们创建一个简单的项目并初始化 Git 仓库：

```bash
# 创建新的项目目录
mkdir my-first-repo
cd my-first-repo

# 初始化 Git 仓库
git init

# 创建一个简单的文件
echo "# My First Git Repository" > README.md

# 查看状态
git status
```

运行 `git status` 会显示 `README.md` 是一个未跟踪的文件：

```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
```

---

## 初始化选项

`git init` 命令还有一些有用的选项：

```bash
# 指定初始分支名称
git init --initial-branch=main
# 或简写为
git init -b main
```

> **TIP** 从 Git 2.28 开始，你可以配置默认分支名称，避免每次都指定。

---

## 你可能会问...

**Q: 我可以在已有文件的目录中运行 git init 吗？**
A: 当然可以！`git init` 不会删除任何现有文件，它只会创建 `.git` 目录。

**Q: 如果我在错误的目录运行了 git init 怎么办？**
A: 你可以简单地删除 `.git` 目录：`rm -rf .git`

---

## RECAP

在本章中，你学习了 Git 版本控制的第一步：初始化仓库。

### 核心概念

- **Git 仓库**: 包含项目文件和版本历史的目录
- **`.git` 目录**: 存储所有 Git 数据的隐藏目录
- **分布式版本控制**: 每个仓库都是完整的项目副本

### 关键命令

- `git init` : 在当前目录初始化新的 Git 仓库
- `git init <目录名>` : 创建新目录并初始化 Git 仓库
- `git init -b <分支名>` : 初始化仓库并指定初始分支名称

### 命令速查表

- `git init` : 初始化当前目录为 Git 仓库
- `git init my-project` : 创建并初始化新项目
- `ls -la` : 查看包括 `.git` 在内的所有文件

### 重要提醒

- 初始化仓库后会创建 `.git` 目录
- **不要手动修改** `.git` 目录中的文件