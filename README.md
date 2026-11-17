# GitHub Learning Notes

This repository records my journey of learning Git and GitHub.

## Learning Objectives

- Understand Git and GitHub.
- Learn Git version control.
- Master Git commands.
- Manage remote repositories.
- Understand GitHub collaboration workflows.
- Learn how to participate in open-source projects.

## Learning Contents

| Chapter | Topic | Status |
|---|---|---|
| 01 | GitHub Basics | In Progress |
| 02 | Git Basics | In Progress |
| 03 | Remote Repository | In Progress |
| 04 | Branch Management | In Progress |
| 05 | GitHub Collaboration | Not Started |
| 06 | Practical Exercises | Not Started |

## Learning Environment

- Operating System: Windows 11
- Git: Git for Windows
- Platform: GitHub

## Learning Records

I will continuously update this repository with learning notes, command examples, and practical exercises.

## 2026-11-13：Git 本地基础操作

### 1. Git 仓库初始化

- `git init`：初始化本地 Git 仓库。
- `git status`：查看当前仓库状态。
- `.git`：保存 Git 仓库的元数据和提交历史。

### 2. Git 的三个区域

- Working Directory（工作区）：实际编辑文件的地方。
- Staging Area（暂存区）：保存下一次提交准备包含的修改。
- Local Repository（本地仓库）：保存已经提交的版本历史。

基本工作流程：

```text
Working Directory
       |
    git add
       |
Staging Area
       |
   git commit
       |
Local Repository
```

### 3. 常用 Git 命令

| 命令 | 作用 |
|---|---|
| `git init` | 初始化仓库 |
| `git status` | 查看仓库状态 |
| `git add` | 添加修改到暂存区 |
| `git commit -m "message"` | 创建提交 |
| `git log --oneline` | 查看提交历史 |
| `git diff` | 查看工作区与暂存区的差异 |
| `git diff --staged` | 查看暂存区与最近提交的差异 |
| `git restore 文件名` | 撤销工作区未暂存的修改 |
| `git restore --staged 文件名` | 取消暂存，保留工作区修改 |
| `git reset --hard` | 将暂存区和工作区重置为最近一次提交的状态；会丢弃未提交的修改 |

### 4. 文件状态

- Untracked：尚未被 Git 跟踪。
- Modified：已经跟踪，但文件内容发生变化。
- Staged：修改已经进入暂存区，等待提交。

### 5. 本课实践总结

完成了本地 Git 仓库初始化、文件创建、暂存、提交、查看提交历史、查看文件差异，以及撤销修改的基础练习。

下一课：Git 分支管理（Branch）。

## 2026-11-14：Git 分支管理

### 1. 分支基础
- 分支用于独立开发不同功能，避免直接影响主线代码。
- master 和 main 都是常见的主分支名称。
- Git 创建分支时，本质上创建一个指向提交的引用。

### 2. 常用命令

| 命令 | 作用 |
|---|---|
| `git branch` | 查看本地分支 |
| `git branch feature` | 创建 feature 分支 |
| `git switch feature` | 切换到 feature 分支 |
| `git switch master` | 切换到 master 分支 |
| `git branch -d feature` | 删除 feature 分支 |
| `git merge feature` | 将 feature 合并到当前分支 |

### 3. 重要知识点
- HEAD 通常指向当前分支。
- 创建分支不会自动切换分支。
- 不同分支可以拥有不同的提交记录。
- 切换分支时，Git 会根据目标提交更新工作区。
- 合并方向由当前所在分支决定。
- Fast-forward 是一种快进合并方式，不需要创建额外的合并提交。

### 4. 本课实践
- 创建 feature 分支。
- 在 feature 分支创建 feature.txt。
- 提交新文件。
- 切换回 master，观察 feature.txt 不存在。
- 使用 git merge 将 feature 合并到 master。

### 5. 本课总结
掌握了 Git 分支的创建、切换、独立开发和合并操作。

下一课：Git 合并冲突（Merge Conflict）。

## 2026-11-16：Git 合并冲突（Merge Conflict）

### 1. 什么是合并冲突？

当两个分支都修改了同一文件的相同位置，而 Git 无法自动判断应该保留哪个版本时，就会产生合并冲突。

### 2. 冲突标记

发生冲突后，Git 会在文件中添加以下标记：

```text
<<<<<<< HEAD
当前分支的内容
=======
被合并分支的内容
>>>>>>> feature
```

- `<<<<<<< HEAD`：当前分支的内容。
- `=======`：两个版本的分隔符。
- `>>>>>>> feature`：被合并分支的内容。

这些标记需要在解决冲突时删除。

### 3. 解决合并冲突的步骤

1. 执行 `git merge feature`，尝试合并分支。
2. 使用编辑器打开冲突文件。
3. 根据实际需求手动修改，保留最终需要的内容。
4. 删除所有冲突标记。
5. 执行 `git add README.md`，标记冲突已解决。
6. 执行 `git commit`，完成合并提交。

### 4. 常用命令

| 命令 | 作用 |
|---|---|
| `git merge feature` | 合并 feature 分支 |
| `git status` | 查看当前仓库状态 |
| `git diff` | 查看文件修改 |
| `git add README.md` | 标记冲突已解决并暂存文件 |
| `git commit -m "Resolve merge conflict"` | 完成合并提交 |
| `git merge --abort` | 放弃尚未完成的合并 |

### 5. Merge Commit

当两个分支分别产生新提交，无法通过 Fast-forward 合并时，Git 通常会创建一个 Merge Commit。

Merge Commit 有两个父提交，分别指向合并前两个分支的最新提交。

可以使用以下命令查看分支合并历史：

```cmd
git log --oneline --graph --decorate --all
```

### 6. 本课实验结果

本次实验在 master 和 feature 分支中分别修改 README.md 的同一位置，成功制造合并冲突。

手动解决冲突后，创建了合并提交：

```text
ae0db89 Resolve merge conflict
```

最终执行 `git status`，得到：

```text
On branch master
nothing to commit, working tree clean
```

说明合并成功，工作区干净。

### 7. 本课核心知识

- Git 不一定能自动解决所有合并冲突。
- 手动修改文件后，需要执行 `git add` 标记冲突已解决。
- Merge Commit 通常有两个父提交。
- `git merge --abort` 可以放弃尚未完成的合并。

## 2026-11-17：Git 远程仓库管理与推送

### 1.本地仓库与远程仓库

- 本地仓库：存储在自己电脑上的 Git 仓库。
- 远程仓库：托管在 GitHub 等平台上的仓库。
- `origin`：远程仓库的默认别名，可以自定义。

查看远程仓库：

```bash
git remote -v
```

### 2.常用远程仓库命令

| 命令 | 作用 |
|---|---|
| `git remote -v` | 查看远程仓库地址 |
| `git ls-remote --heads origin` | 查看远程分支及其提交 |
| `git fetch` | 获取远程数据，不自动合并 |
| `git pull` | 获取远程数据并整合到当前分支 |
| `git push` | 推送本地提交到远程仓库 |

### 3.本地分支与远程跟踪分支

例如：

```text
本地分支：master
远程跟踪分支：origin/main
远程实际分支：GitHub 上的 main
```

- `master`：本地普通分支。
- `main`：远程仓库中的实际分支。
- `origin/main`：本地的远程跟踪分支，用于记录最近一次获取到的远程 main 分支位置。
- `origin`：远程仓库的别名。

远程跟踪分支不等于远程服务器上的实际分支。

### 4.HEAD 与分支的关系

`HEAD` 是 Git 中指向当前工作位置的特殊引用。

当当前处于 master 分支时：

```text
HEAD → master → 最新提交
```

因此：

```bash
git push origin HEAD:main
```

表示将当前分支所指向的提交推送到远程 main 分支。

### 5.推送分支

将本地 master 推送到远程 main：

```bash
git push origin master:main
```

将本地 feature 推送到远程 feature，并建立上游跟踪关系：

```bash
git push -u origin feature:feature
```

其中：

- `-u`：建立上游跟踪关系。
- `origin`：远程仓库别名。
- 第一个 `feature`：本地分支。
- 第二个 `feature`：远程目标分支。

建立上游关系后，通常可以直接使用 `git push` 和 `git pull`。

### 6.push.default=simple 与分支名称不一致

Git 默认的 `push.default=simple` 推送策略要求当前分支名称与上游分支名称一致。

例如：

```text
本地 master → 远程 origin/main
```

由于名称不同，直接执行：

```bash
git push
```

可能报错。

可以明确指定目标：

```bash
git push origin HEAD:main
```

### 7.本课实践记录

本地仓库：GitHub-Practice

远程仓库：GitHub-Practice

本地分支：master

远程分支：main

本地最新提交：

```text
ae0db89 Resolve merge conflict
```

通过以下命令验证本地和远程提交是否一致：

```bash
git ls-remote --heads origin
git log -1 --oneline
```

两边提交哈希一致，说明本地 master 和远程 main 指向同一个提交。

### 8.本课总结

1. 理解本地仓库与远程仓库的区别。
2. 掌握 fetch、pull、push 的区别。
3. 理解远程跟踪分支 origin/main。
4. 理解 HEAD 与当前分支的关系。
5. 掌握将本地分支推送到不同名称的远程分支。
6. 掌握使用 `-u` 建立上游跟踪关系。
