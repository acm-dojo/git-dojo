将修改后的代码提交到 Git 仓库需要几步？

使用 `git add` 和 `git commit`让  Git 跟踪你的所有修改。

---

## 理解 Git 的三个区域

在学习 `git add` 和 `git commit` 之前，必须先理解 Git 管理文件的三个核心区域：

1.  **工作区 (Working Directory)**: 用户在电脑上能直接看到和编辑的项目文件夹。
2.  **暂存区 (Staging Area / Index)**: 一个临时的缓冲区，记录**下一次**准备提交的文件快照。
3.  **版本库 (Repository)**: `.git` 目录，永久存储了项目所有版本历史的地方。

`git add` 将工作区的更改放入暂存区，而 `git commit` 则将暂存区的内容打包存入版本库。

---

## git add 命令

`git add` 命令将工作区中某个文件或目录的当前更改放入暂存区，包含在**下一次提交**中，让用户能够精确控制每次提交的内容。

### 使用场景

1. **跟踪新文件**: 在 Git 工作区中新建一个文件时，其状态为 `Untracked`，只有使用 `git add <file>` 后 Git 才会开始追踪并管理该文件。
    ```bash
    # 创建一个新文件
    echo "Hello, Git!" > README.md

    # 查看状态，会提示 README.md 是未跟踪文件(Untracked files)
    git status

    # 使用 git add 开始跟踪它
    git add README.md

    # 再次查看状态，会提示 README.md 已被暂存，准备提交(Changes to be committed)
    git status
    ```
2. **暂存已修改文件**: 修改已被 Git 跟踪的文件后，使用 `git add <filename>` 将修改添加到暂存区。
    ```bash
    # 修改 README.md
    echo "Add a new line." >> README.md

    # 查看状态，会提示 README.md 有未暂存的修改(Changes not staged for commit)
    git status

    # 将修改添加到暂存区
    git add README.md

    # 再次查看状态，提示修改已暂存
    git status
    ```

### 基本用法
``` bash
# 添加指定文件:
git add <file>

# 添加指定目录下的所有更改:
git add src/

# 添加当前目录所有更改:
git add .

# 交互式添加: 使用 `-p` 或 `--patch` 标志，Git 会逐一展示文件中的每一处修改（称为 "hunk"），让你决定是否要暂存它。
git add -p <file>/<directory>/.

```

---

## git commit 命令

将暂存区中的内容打包，生成一个永久的版本记录并存入版本库，同时通过`commit message`为本次提交附加说明。简言之，每次提交都相当于项目历史中的一个“存档点”。

### 基本用法
``` bash 
# 使用 `-m` (message) 标志：通过命令行直接提供信息
git commit -m "feat: Add README.md"

# 打开文本编辑器编写信息：如果不带参数，Git 会自动打开配置的默认文本编辑器（如 Nano、Vim），让用户编写更详细的提交信息。
git commit "空行"

```

### **commit message**

一次好的提交应只处理一个问题，而一个好的提交信息应该清晰地说明本次提交“做了什么”以及“为什么这么做”。

**良好实践 (Conventional Commits 规范):**

一个有所简化的标准的提交信息格式如下：
```
<类型>: <简短描述>

[可选的正文]
```
-   **类型 (Type)**: 如 `feat` (新功能), `fix` (修复bug), `docs` (文档), `style` (格式), `refactor` (重构), `test` (测试), `chore` (构建或杂务)。
-   **简短描述**: 50个字符以内，清晰概括本次提交。
-   **正文 (Body)**: 可选，正文必须起始于描述字段结束的一个空行后，每行不超过72个字符，并可以使用空行分隔不同段落。提交的正文内容自由编写。

例子:
```bash
git commit "fix: Remove null pointer dereference in user login"
```

更具体的规范可见： [Conventional Commits 规范](https://www.conventionalcommits.org/zh-hans/v1.0.0/)

## RECAP

### 核心概念

**工作区 -> 暂存区 -> 版本库**: 这是 Git 提交的核心流程。

**git add**: 将选定的工作区中修改放进暂存区。

**git commit**: 将暂存区中所有修改打包并附上信息，永久地存入版本库历史中。

### 关键命令
-   `git add <file>`: 将指定文件的更改添加到暂存区。
-   `git add <directory/>`: 将指定目录下的所有更改添加到暂存区。
-   `git add .`: 将当前目录下所有更改添加到暂存区。
-   `git add -p`: 交互式地选择要暂存的修改部分。
-   `git commit -m "message"`: 将暂存区内容附上简短信息，并提交到版本库。
-   `git commit`: 打开编辑器编写详细的提交信息。

---

## 任务卡

进入仓库`~/dojo-add-commit`，仓库已初始化，文件结构如下：
```
include/
  book.hpp
  user.hpp
src/
  main.cpp
  book/
    book1.cpp
    book2.cpp
  user/
    user.cpp
CMakeLists.txt
```
请使用 `git add` 命令将工作目录下所有修改过的文件加入暂存区，并提交以下文件：
   - include/book.hpp
   - src/book/book1.cpp
   - src/book/book2.cpp
  
只允许进行一次提交，且其它文件不能出现本次提交中。提交完成后运行 `/challenge/submit` 检查你的结果是否符合要求。
