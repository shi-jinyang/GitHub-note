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
| 03 | Remote Repository | Not Started |
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
