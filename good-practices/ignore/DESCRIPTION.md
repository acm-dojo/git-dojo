不想让测试点与编译产物出现在 github 仓库中怎么办？

可以使用 `.gitignore` 文件让 Git “选择性失明”。

---

## 什么是.gitignore文件？其作用是什么？

`.gitignore` 文件是 Git 仓库中的一个文本文件，告诉 Git 哪些文件或目录不需要被跟踪和提交到版本库中。它的主要作用是防止不必要的文件，包括测试点、编译产物等被添加到 Git 仓库中，从而保持仓库的整洁和高效。

例 1 ：
某些大作业的测试点大小可能高达 500 MB ，如果我们将测试点解压到 Git 仓库 `main` 分支的 `testcases/` 目录下并提交，会遭遇如下问题：
``` bash
git add.
git commit -m "chore: add testcases."
git push origin main

remote: Resolving deltas: 100% (1/1), done.
......
remote: error: File testcases/your_large_file.dat is 1.00 GB; this exceeds GitHub's file size limit of 100.00 MB
......
```
而我们可以通过在 `.gitignore` 文件中添加 `testcases/` 目录避免这个问题：
``` .gitignore
# 忽略 testcases 目录
testcases/
```

例 2 ：
与其将C++编译出的 `.o` 等编译产物提交到 Git 仓库中乃至提交到 github 上，不如只用 Git 管理并提交源代码文件，通过编译重新生成可执行代码。
``` .gitignore
# 忽略所有 .o 文件
*.o
```


> **注意：** `.gitignore` 文件只会对 Git 未跟踪的文件起效。如果你已经将某个文件通过 git add 添加到 Git 仓库中（即已经被跟踪），那么即使你在 `.gitignore` 文件中忽略它，Git 仍然会继续跟踪该文件的更改。
> 
> 例子：
> ``` bash
> # 创建两个日志文件
> touch a.log b.log
>
> # 将 a.log 添加到暂存区，使其变为“已跟踪”状态
> git add a.log
>
> # 查看当前状态，a.log 已暂存，b.log 未跟踪
> git status
>
> # 输出（部分省略）:
> Changes to be committed:
>        new file:   a.log
>
> Untracked files:
>        b.log
>
> # 创建 .gitignore 文件，忽略所有 .log 文件
> echo "*.log" >> .gitignore
>
> # 再次查看状态
> git status
>
> # 输出:
> Changes to be committed:
>         new file:   a.log  
>
> Untracked files:
>         .gitignore 
>
> # 解释：a.log 依然被跟踪，而b.log 因为从未被跟踪成功被.gitignore忽略。.gitignore 文件本身是新文件
>```

---

## .gitignore文件常用语法
`.gitignore` 文件中的每一行都指定了一个忽略的对象。

1. **注释**: 以 `#` 开头的行是注释，并无实际作用。
    ```gitignore
    # 这是一个注释
    ```

2. **忽略目录**: 在模式的末尾加上斜杠 `/` 表示一个目录。Git 会忽略该目录下的所有文件和子目录。
    ```gitignore
    # 忽略 build/ 目录
    build/
    ```

3. **使用通配符**:
  * `*` 匹配零个或多个字符。
    ```gitignore
    # 忽略所有以 .log 结尾的文件
    *.log 

    # 忽略所有以 .o 结尾的文件
    *.o
    ```
  * `?` 匹配一个任意字符。
    ```gitignore
    # 忽略 a.cpp, b.cpp, 但不忽略 abc.cpp
    ?.cpp
    ```
  * `**` 匹配任意中间目录。
    ```gitignore
    # 忽略任何目录下名为 logs 的文件夹
    **/logs/

    # 忽略任何目录下以 .o 结尾的文件
    **/*.o
    ```

4.  **否定模式 (例外规则)**: 在模式前加上感叹号 `!` 表示不忽略，可用于为一个更广泛的忽略规则设置例外。
    ```gitignore
    # 忽略所有 .log 文件...
    *.log

    # ...但 important.log 文件除外
    !important.log
    ```
    >**注意**：如果一个文件的父目录已经被忽略，那么你无法通过否定模式来单独保留这个文件。例如，`build/` 被忽略后，`!build/main.o` 是无效的。

---

## RECAP

### 核心概念

- **`.gitignore` 的作用**: 定义 Git 在扫描工作目录时应该忽略的文件和目录模式，防止不必要的文件进入版本控制。
- **只对未跟踪文件有效**: `.gitignore` 无法忽略已经通过 `git add` 命令纳入版本控制的文件，因此最好在项目开始时设置好 `.gitignore` 文件。

### 关键操作

- **创建 `.gitignore` 文件**: 在项目根目录创建名为 `.gitignore` 的文本文件。
- **添加忽略规则**: 每行写一个模式，可以使用 `#` 添加注释，使用 `*` 等通配符等。

### .gitignore语法速查表

- `*[suffix，包括.log/.o/.exe等]`: 忽略特定后缀文件。
- `[case，如build]/`: 忽略特定目录及内部所有内容。
- `![file]`: 不要忽略某个文件。

---

## 任务卡

修改`.gitignore`文件，使仓库正确忽略指定的文件和目录，并确保重要文件仍然被跟踪和提交。

具体步骤如下：

1. 进入仓库`~/dojo-ignore`并编辑仓库中已存在的 `.gitignore` 文件，从而使如下文件被忽略：
   - 除 `important.log` 外所有以`.log`结尾的文件。
   - `temp/` 目录下所有内容。
   - `src` 下的 `.o` 文件。
   - `ignore.txt`。
  
    同时请保证其他文件不被忽略。

2. 进行一次`commit`提交其他文件，请确保提交后工作区无未提交或未跟踪文件。

3. 运行 `/challenge/submit` 检查 `.gitignore` 是否生效，效果是否正确。
