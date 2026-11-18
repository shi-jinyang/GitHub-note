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

## 2026-11-18：Git 分支协作与 Pull Request

### 1. 本课学习目标

- 理解远程 feature 分支与 Pull Request 的关系。
- 掌握 GitHub Pull Request 的创建和合并流程。
- 理解 base、compare 和 Diff。
- 理解 Merge commit 的结构。
- 掌握 GitHub 合并后同步本地仓库的方法。
- 初步了解 Merge commit、Squash merge 和 Rebase。

### 2. 实际操作记录

#### 2.1 推送 feature 分支

```cmd
git switch feature
git push -u origin feature
```

`-u` 用于建立本地分支与远程跟踪分支的关联。

本次建立的关联：

```text
feature -> origin/feature
```

#### 2.2 在 feature 分支开发新功能

创建文件：

```cmd
echo This is a new feature for PR practice. > feature-demo.txt
```

提交：

```cmd
git add feature-demo.txt
git commit -m "add feature demo for PR"
git push
```

本次提交：

```text
6563c8e add feature demo for PR
```

#### 2.3 创建 Pull Request

本次 PR：

- PR 编号：#1
- 标题：add feature demo for PR
- base：main
- compare：feature

PR 的含义是：请求将 feature 分支的变更合并到 main 分支。

**base 和 compare：**

- base：目标分支，即希望合并到哪个分支。
- compare：来源分支，即提供变更的分支。

如果把两者反过来，就会变成请求将 main 的变更合并到 feature。

#### 2.4 理解 Diff

Diff 用于展示两个分支之间的文件差异：

- `+`：新增内容。
- `-`：删除内容。
- `--- /dev/null`：表示原来不存在该文件。
- `+++ b/feature-demo.txt`：表示新文件路径。

本次 PR 新增了 `feature-demo.txt`，因此 Diff 显示一行 `+`。

#### 2.5 Mergeable 的含义

GitHub 显示 Mergeable，通常表示当前分支可以合并，没有已知的合并冲突。

但不代表：

- 已经通过人工 Code Review。
- 代码逻辑一定正确。
- 程序没有 Bug。
- 自动化测试一定通过。

因此，合并前仍然需要检查代码和测试结果。

### 3. Pull Request 合并

本次在 GitHub 上使用 Create a merge commit 完成合并。

PR #1 已成功合并：

```text
PR #1: add feature demo for PR
Merge commit: b75a9fb
```

### 4. Merge commit 的结构

本次提交历史：

```text
*   b75a9fb (HEAD -> master, origin/main) Merge pull request #1
|\
| * 6563c8e (origin/feature, feature) add feature demo for PR
* | ae0db89 Resolve merge conflict
|\|
| * 5fa5187 Update README on feature
* | edcfacb Update README on master
|/
* fe0987f Add feature branch file
* 7a2a676 Add second and third lesson notes
* a210890 Initial commit
```

Merge commit 通常有两个父提交：

- 第一父提交：合并前目标分支的提交，本次为 `ae0db89`。
- 第二父提交：来源分支的提交，本次为 `6563c8e`。

查看当前提交及父提交：

```cmd
git rev-list --parents -n 1 HEAD
```

普通提交通常只有一个父提交，Merge commit 通常有两个父提交。

### 5. GitHub 合并后同步本地仓库

本次执行：

```cmd
git switch master
git pull
```

本地 master 跟踪远程 origin/main，因此 `git pull` 会同步远程 main 的更新。

检查提交历史：

```cmd
git log --oneline --graph --decorate --all
```

检查工作区：

```cmd
git status
```

最终状态：

```text
On branch master
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

说明本地 master 已经与远程 main 同步，工作区干净。

### 6. 三种常见合并方式

#### 6.1 Merge commit

```cmd
git merge feature
```

- 保留分支历史。
- 创建合并提交。
- 通常有两个父提交。

#### 6.2 Squash merge

```cmd
git merge --squash feature
git commit -m "Squash feature changes"
```

- 将 feature 的改动汇总到当前分支工作区。
- 不自动创建双父提交的 Merge commit。
- 需要手动执行 git commit。
- 新提交通常只有一个父提交。

#### 6.3 Rebase

```cmd
git rebase main
```

- 将当前分支的提交重新应用到 main 最新提交之后。
- 通常会改变被重新应用提交的哈希。
- 不创建传统的双父提交 Merge commit。

### 7. 本课思考题

1. Merge commit b75a9fb 有几个父提交？

   答案：2 个。

2. 执行 git pull 后，为什么本地 master 能看到 feature 的提交？

   答案：因为远程 main 已经包含了 feature 的合并结果，git pull 将远程 main 的更新同步到了本地 master。

3. git merge --squash 与普通 Merge commit 有什么区别？

   答案：Squash 将 feature 的改动汇总成待提交的内容，不自动创建双父提交的 Merge commit，需要手动提交。

### 8. 本课总结

本课完成了一次完整的 GitHub 分支协作流程：

1. 创建并推送远程 feature 分支。
2. 在 feature 分支开发新功能。
3. 创建 Pull Request。
4. 理解 base、compare 和 Diff。
5. 检查 PR 并在 GitHub 上合并。
6. 使用 git pull 同步远程合并结果。
7. 使用 git log --graph 查看合并历史。
