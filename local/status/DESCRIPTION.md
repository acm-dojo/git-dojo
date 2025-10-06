项目里有100个文件，忘了自己修改过哪些应该怎么办？

可以使用 `git status` 与 `git diff` 查看项目情况。

---

## git status 命令

`git status` 能快速输出当前项目的状态：有哪些文件被修改了？有哪些文件已暂存？位于哪个分支？本地分支与远程分支是否同步？（分支相关内容详情见branch一节）

### 基本用法
``` bash
# 该命令会向输出流中打印项目状态
git status
```

### 输出解读
一个典型的 `git status` 输出包含关于当前分支用户需要的所有信息：

```bash
# 1. 项目当前所在分支
On branch main

# 2. 本地分支与远程分支的关系
# "Your branch is up to date with 'origin/main'." -> 本地与远程同步，一切正常。
# "Your branch is ahead of 'origin/main' by X commits." -> 本地有X个新提交尚未推送到远程。
# "Your branch is behind 'origin/main' by Y commits." -> 远程有Y个新提交需要拉取到本地。
Your branch is up to date with 'origin/main'.

# 3. 已暂存的更改(位于Staging Area)
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    modified:   user.cpp

# 4. 已修改但未暂存的更改
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
    modified:   book.cpp
                book.hpp

# 5. 未被 Git 跟踪的新文件
Untracked files:
  (use "git add <file>..." to include in what will be committed)
            logger.hpp
```

---

## git diff 命令

`git status`显示状态信息的最小单位是文件，而 `git diff` 可以精确地输出文件**具体哪一行、哪个字符**发生了变化。

### 基本用法

`git diff` 是一个多功能的比较工具，使用时需要指定比较的对象。

1.  **比较“工作区”与“暂存区”**:
    这是 `git diff` 最常见的用法。它会显示所有**已修改但未暂存**的改动。
    ```bash
    # 查看所有未暂存的修改
    git diff
    
    # 只看特定文件的未暂存修改
    git diff book.hpp
    ```

2.  **比较“暂存区”与“版本库”**:
    使用 `--staged` 标志，可以查看**已暂存但未提交**的改动。
    ```bash
    git diff --staged
    ```

3.  **比较“工作区”与“版本库”**:
    比较你当前工作区的所有修改（无论是否暂存）与最近一次提交的版本有何不同。
    ```bash
    git diff HEAD
    ```

4. **其他**:
    事实上,`git diff`还可以比较很多内容，同学们有需要可以自行查询。

### 输出解读

```diff
diff --git a/book.cpp b/book.cpp
index 6b9195f..8b832a2 100644
--- a/book.cpp
+++ b/book.cpp
@@ -1,4 +1,4 @@
-  #include<bits/stdc++.h>;
+  #include<stdint.h>;
;
```
-   `--- a/book.cpp`: 代表修改前的源文件 (`a` 文件)。
-   `+++ b/book.cpp`: 代表修改后的目标文件 (`b` 文件)。
-   `@@ ... @@`: 指明修改发生在文件的哪几行。
-   `-` (减号): 表示这一行从源文件中被**删除**了。
-   `+` (加号): 表示这一行在目标文件中是**新增**的。
> **TIPS**:使用 `q` 键退出diff查看界面。

---

## RECAP

### 核心概念

-   **`git status`**: 输出项目的整体状态。
-   **`git diff`**: 输出文件的具体变化。
-   **`git diff`比较不同的区域**: `git diff` 通过调整flag可以灵活比较 Git 三大区域（工作区、暂存区、版本库）之间的差异。

### 关键命令

-   `git status`: 查看项目当前状态。
-   `git diff`: 查看**未暂存**的修改。
-   `git diff --staged`: 查看**已暂存**、待提交的修改。
-   `git diff HEAD`: 查看所有**未提交**的修改（包含已暂存和未暂存）。

---

### 任务卡
调整仓库到如果使用 `git status` 命令会输出如下结果（忽略日期和提示，内容结构需一致）：

```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   src/main.cpp
        new file:   src/book/book.cpp

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   include/user.hpp

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        src/user/user.cpp
        CMakeLists.txt
```

调整后运行 `/challenge/submit` 检测仓库状态。
