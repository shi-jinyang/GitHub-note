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

## 2026-11-19：Git Rebase 原理与实战

### 1.学习目标

- 理解 Git Rebase 的基本原理。
- 掌握 Rebase 与 Merge 的区别。
- 掌握 `git rebase` 的基本使用方法。
- 学会处理 Rebase 过程中的冲突。
- 理解为什么不应该随意 Rebase 公共分支。

### 2.Rebase 基本原理

Rebase 的作用是将当前分支上的提交重新应用到目标分支的最新提交之后。

基本命令：

```bash
git switch feature
git rebase master
```

注意：

- 被重新整理的是当前分支。
- 目标分支不会因为 Rebase 而被改写。
- Rebase 通常会产生新的提交哈希。
- Rebase 不代表已经将当前分支合并到目标分支。

### 3.Rebase 实验

本次实验创建了本地练习分支：

```bash
git switch -c rebase-practice master
```

在练习分支上创建提交：

```text
897b53f add first rebase practice commit
```

随后在 master 分支上创建新提交：

```text
49234ce add commit on master
```

切回练习分支并执行：

```bash
git switch rebase-practice
git rebase master
```

Rebase 成功后，原提交被重新应用，哈希发生变化。

### 4.Rebase 冲突处理实验

本次制造了 `add/add` 类型冲突：

- master 分支创建并修改 `conflict-demo.txt`。
- rebase-practice 分支独立创建同名文件。
- 执行 `git rebase master` 时发生冲突。

冲突解决步骤：

```bash
# 编辑冲突文件，保留需要的内容
git add conflict-demo.txt
git rebase --continue
```

本次最终文件内容：

```text
master version

feature version
```

最终提交历史关键部分：

```text
* 7459fbd (HEAD -> rebase-practice) modify conflict demo on feature
* 7d7630d add first rebase practice commit
* db6ad3a (master) modify conflict demo on master
* 869c170 add conflict demo base
* 49234ce add commit on master
```

实验结果：

- Rebase 成功完成。
- 原提交被重新创建，哈希发生变化。
- master 分支没有被改写。
- `git status` 显示工作区干净。

### 5.Rebase 相关命令

| 命令 | 作用 |
|---|---|
| `git rebase master` | 将当前分支提交重新应用到 master 后面 |
| `git rebase --continue` | 解决冲突后继续 Rebase |
| `git rebase --abort` | 放弃本次 Rebase |
| `git rebase --skip` | 跳过当前正在重放的提交 |

### 6.Rebase 与 Merge 的区别

- Merge：合并分支，通常保留原有分支历史。
- Rebase：重新应用提交，通常形成线性历史。
- Rebase 会改变被重新应用提交的哈希。
- 不要随意 Rebase 已经被其他开发人员使用的公共分支。

### 7.本课总结

本课完成了 Rebase 的原理学习、无冲突实验和冲突处理实验，掌握了 Rebase 的基本操作流程。

## 2026-11-20：Git Reset 与 Git Revert

### 1.学习目标

- 理解 Git 的 HEAD、工作区、暂存区和本地仓库。
- 掌握 `git reset` 的三种模式。
- 理解 `git revert` 的工作原理。
- 理解 Reset 与 Revert 的区别。
- 掌握不同场景下撤销提交的方法。

### 2.Git Reset

`git reset` 的核心作用是移动当前分支的 HEAD 指针到指定提交，并根据模式决定是否重置暂存区和工作区。

基本命令：

```bash
git reset HEAD~1
```

表示将当前分支回退到上一个提交。

#### 2.1 --soft

```bash
git reset --soft HEAD~1
```

- HEAD 移动。
- 暂存区保留修改。
- 工作区保留修改。

实验结果：撤销 Version 3 提交后，Version 3 的修改仍然保留在暂存区。

#### 2.2 --mixed

```bash
git reset --mixed HEAD~1
```

- HEAD 移动。
- 暂存区重置。
- 工作区保留修改。

实验结果：Version 3 的修改从暂存区变成工作区中的未暂存修改。

注意：`--mixed` 是 Git Reset 的默认模式。

#### 2.3 --hard

```bash
git reset --hard HEAD~1
```

- HEAD 移动。
- 暂存区重置。
- 工作区重置。

实验结果：Version 3 的未提交修改被丢弃，文件恢复为 Version 2。

注意：`--hard` 可能造成未提交修改丢失，使用前必须检查工作区状态。

### 3.Git Revert

`git revert` 不会删除原提交，而是创建一个新的提交，用于抵消指定提交带来的修改。

基本命令：

```bash
git revert HEAD
```

本次实验：

原提交：

```text
5c0aea7 add reset demo version 3 again
```

撤销后：

```text
884d1aa Revert "add reset demo version 3 again"
5c0aea7 add reset demo version 3 again
```

实验结果：

- 原提交仍然保留在历史中。
- Git 创建了新的撤销提交。
- 文件中的 Version 3 被删除。
- 工作区干净。

### 4.Reset 与 Revert 的区别

| 对比 | Reset | Revert |
|---|---|---|
| 工作方式 | 移动 HEAD | 创建新的反向提交 |
| 是否改写当前分支历史 | 是 | 否 |
| 原提交是否保留在当前历史中 | 通常不再属于当前分支历史 | 保留 |
| 常见使用场景 | 本地提交整理 | 已推送或多人协作 |

### 5.实际使用建议

1. 本地尚未共享的错误提交，可以考虑使用 Reset。
2. 已经推送到远程、其他人可能已经拉取的提交，通常优先使用 Revert。
3. 使用 `git reset --hard` 前，务必确认没有需要保留的未提交修改。

### 6.本课实验结果

实验分支：`reset-practice`

实验文件：`reset-demo.txt`

完成的实验：

- 创建 Version 1、Version 2、Version 3 三个版本。
- 使用 `git reset --soft` 撤销提交，观察暂存区保留修改。
- 使用 `git reset --mixed` 重置暂存区，观察工作区保留修改。
- 使用 `git reset --hard` 丢弃未提交修改。
- 重新创建 Version 3 提交。
- 使用 `git revert HEAD` 创建反向提交，成功撤销 Version 3。

## 2026-11-22：Git Reflog —— 找回丢失的提交

### 1.本课学习目标

1. 理解 Git Reflog 的作用。
2. 掌握 `git reflog` 和 `HEAD@{n}`。
3. 理解 Reflog 与 `git log` 的区别。
4. 学会恢复被 `git reset --hard` 移出当前分支历史的提交。

### 2.核心知识点

#### 2.1 git log 与 git reflog

- `git log`：查看从当前引用出发能够访问到的提交历史。
- `git reflog`：查看本地 HEAD 和其他引用的变化历史。
- `HEAD@{0}`：最近一次 HEAD 变化。
- `HEAD@{1}`：上一次 HEAD 变化。

Reflog 不只是记录 commit，还会记录 reset、checkout、rebase 等操作导致的引用变化。

#### 2.2 git reset --hard 与提交对象

执行：

```bash
git reset --hard HEAD~2
```

会移动当前分支引用，并重置暂存区和工作区。

原来的提交不再属于当前分支历史，但提交对象不一定立即被删除。

#### 2.3 使用 Reflog 恢复提交

实验中，Reset 前的提交：

```text
3259750 Version 3
c131e78 Version 2
201659a Version 1
```

执行 `git reset --hard HEAD~2` 后，当前分支回退到：

```text
201659a Version 1
```

通过：

```bash
git reflog -10
```

找到了原来的 Version 3 提交：

```text
3259750 HEAD@{1}: commit: add reflog demo version 3
```

创建恢复分支：

```bash
git branch reflog-recovered 3259750
git switch reflog-recovered
```

恢复成功，文件内容重新变为：

```text
Version 1
Version 2
Version 3
```

### 3.本课实验结果

- 成功创建三个连续提交。
- 成功查看 Reflog。
- 成功模拟 `git reset --hard HEAD~2` 误操作。
- 成功通过 Reflog 找到原来的提交。
- 成功创建 `reflog-recovered` 分支。
- 成功恢复 Version 1、Version 2、Version 3。
- 最终工作区干净，恢复分支指向 `3259750`。

### 4.重要注意事项

1. Reflog 是本地记录，不会自动推送到远程仓库。
2. Reflog 有过期机制，不是永久备份。
3. 发现误操作后应尽快恢复提交。
4. 推荐先使用 `git branch` 创建恢复分支，避免直接使用 `reset --hard` 覆盖当前工作区。

## 2026-11-23：Git 底层对象模型

### 1.本课学习目标

理解 Git 的底层对象存储机制，掌握 Blob、Tree、Commit、Tag 四种核心对象及其关系。

### 2.Git 的四种核心对象

2.2 **Blob Object**
   - 保存文件内容，不保存文件名和目录路径。
   - 相同内容会生成相同的 Blob 哈希。
   - 文件内容发生变化时，会生成新的 Blob 对象，旧对象不会被直接修改。

2.2 **Tree Object**
   - 保存目录结构。
   - 记录文件名、文件模式、对象类型及对象哈希。
   - 可以指向 Blob 或其他 Tree。

2.3 **Commit Object**
   - 指向项目快照的根 Tree。
   - 保存父提交、作者、提交者、时间和提交说明。
   - 每个 Commit 逻辑上描述完整项目快照。

2.4 **Tag Object**
   - 附注标签对应一个 Tag Object。
   - 保存目标对象、目标类型、标签名、创建者、时间和标签说明。

### 3.Git 对象之间的关系

```text
Commit
  |
  v
Root Tree
  |
  +---- Blob
  |
  +---- Blob
  |
  +---- Sub Tree
          |
          +---- Blob

Annotated Tag
  |
  v
Tag Object
  |
  v
Commit
```

轻量标签只是引用，直接指向 Commit；附注标签则指向 Tag Object。

### 4.实际实验记录

在 Windows CMD 和 GitHub-Practice 仓库中完成以下实验：

1. 使用 `git cat-file -t` 查看对象类型。
2. 使用 `git cat-file -p` 查看 Commit、Tree、Tag 和 Blob 内容。
3. 使用 `git hash-object` 计算文件内容的哈希。
4. 使用 `git hash-object -w` 将 Blob 写入对象数据库。
5. 验证相同内容生成相同哈希。
6. 修改文件内容，验证新内容生成新的 Blob。
7. 使用 `git add` 将文件加入暂存区。
8. 使用 `git write-tree` 将整个暂存区写成 Tree Object。
9. 创建轻量标签 `v1.0` 和附注标签 `v2.0`，比较二者的底层区别。

### 5.关键实验结果

- `Hello Git!` 对应 Blob 哈希：
  `14a4db2254d0aa7a9f882e528582d1afde6ff2ce`
- `Hello Git!!` 对应 Blob 哈希：
  `32826a5a5ddce1c39a03cddcf4613f8d65bd999b`
- 两个内容相同的文件生成相同 Blob 哈希。
- `git write-tree` 生成的 Tree 哈希：
  `7ed4fb6ab76b7885a3f8d092910ede5c06efa5c9`
- `git cat-file -t v1.0` 输出 `commit`。
- `git cat-file -t v2.0` 输出 `tag`。

### 6.本课总结

Git 使用内容寻址的对象数据库组织项目历史。

Commit 指向 Tree，Tree 指向 Blob 或子 Tree。相同内容可以复用已有 Blob，因此 Git 虽然逻辑上为每次提交保存完整快照，但不需要重复存储所有未变化的文件内容。

### 7.实验现场状态

- `hash-demo.txt` 和 `hash-demo-2.txt` 已创建，当前保留在工作区。
- 两个文件已从暂存区撤销，当前为未跟踪文件。
- Blob 和 Tree 对象实验已完成。

## 2026-11-24：Git 引用系统、HEAD 与分支的底层关系

### 1.本课学习目标

理解 Git Reference（引用）的概念，掌握分支、HEAD、Detached HEAD 的底层关系，了解 Reflog 的存储结构，以及 Loose refs、Packed refs 和 `git update-ref`。

### 2.核心知识点

#### 2.1 Git 引用（Reference）

- 引用为 Git 对象提供可读名称。
- 本地分支引用：`refs/heads/`
- 标签引用：`refs/tags/`
- 远程跟踪引用：`refs/remotes/`
- 分支本质上是指向 Commit 的可移动引用，不是代码副本。

#### 2.2 HEAD 与 Attached HEAD

- Attached HEAD：`.git/HEAD` 保存 `ref: refs/heads/分支名`。
- HEAD 通过分支引用间接指向 Commit。
- 在 Attached HEAD 状态下创建提交，当前分支引用和 HEAD 最终指向的新 Commit 一起移动。

#### 2.3 Detached HEAD

- Detached HEAD：`.git/HEAD` 直接保存 Commit 哈希。
- 可以在 Detached HEAD 状态下创建提交。
- 创建提交时 HEAD 移动，但原分支引用不会自动移动。
- 可以使用 `git switch -c 新分支名` 创建分支保存当前提交。

#### 2.4 Reflog

- Reflog 记录本地引用的移动历史。
- `git reflog` 查看 HEAD 的移动记录。
- `git reflog show 分支名` 查看指定分支的 Reflog。
- `.git/logs/HEAD` 保存 HEAD Reflog。
- `.git/logs/refs/heads/分支名` 保存对应分支的 Reflog。
- Reflog 不会自动同步到远程仓库。

Reflog 每条记录包含：
- 旧对象哈希
- 新对象哈希
- 操作者
- 时间戳
- 时区
- 操作说明

#### 2.5 Loose refs 与 Packed refs

- Loose refs：引用分别保存在独立文件中。
- Packed refs：多个引用集中保存在 `.git/packed-refs`。
- Git 可以根据需要管理引用的存储形式。
- 引用打包与 Git 对象打包是不同概念。

#### 2.6 git update-ref

- `git update-ref <refname> <new-val>`：创建或更新引用。
- `git update-ref -d <refname>`：删除引用。
- `-m`：为引用更新添加说明。
- 不建议手动修改 `.git` 内部引用文件，应使用 Git 提供的命令。

### 3.实际实验记录

1. 查看 `.git/HEAD`，确认 HEAD 指向 `reflog-recovered`。
2. 查看 `.git/refs/heads/reflog-recovered`，确认其指向 Commit `3259750`。
3. 查看标签引用，验证轻量标签直接指向 Commit，附注标签指向 Tag Object。
4. 使用 `git checkout <commit-hash>` 进入 Detached HEAD。
5. 在 Detached HEAD 状态下创建 Commit `a7114ff`。
6. 验证 HEAD 移动到 `a7114ff`，原来的 `reflog-recovered` 仍指向 `3259750`。
7. 使用 `git switch -c detached-recovered` 创建新分支，成功保存 `a7114ff`。
8. 使用 `git reflog -8` 查看 HEAD 移动历史。
9. 使用 `git reflog show reflog-recovered` 查看指定分支的 Reflog。
10. 查看 `.git/logs/HEAD` 和 `.git/logs/refs/heads/reflog-recovered`，分析 Reflog 文件格式。
11. 检查 `.git/packed-refs`，本次实验中该文件不存在。
12. 使用 `git update-ref -h` 查看引用管理命令帮助。
13. 使用 `git rev-parse HEAD` 和 `git show-ref --heads` 验证 HEAD 与本地分支引用的关系。

### 4.实验结果

- Detached HEAD 下成功创建提交 `a7114ff`。
- 成功创建 `detached-recovered` 分支保存该提交。
- 原有 `reflog-recovered` 仍指向 `3259750`，未被移动。
- 成功区分 HEAD Reflog 和分支 Reflog。
- 本次没有执行 `git update-ref` 的实际修改操作，仅查看了帮助信息。

## 2026-11-26：Git 配置系统（System、Global、Local 与配置优先级）

### 1.学习目标

- 理解 Git 的三种配置作用域。
- 掌握不同配置作用域的优先级。
- 学会查看配置来源、设置和删除配置。
- 理解 Git 多值配置。
- 学会使用 Git 命令别名。

### 2.核心知识点

#### 2.1 三种配置作用域

| 作用域 | 参数 | 配置文件 | 影响范围 |
|---|---|---|---|
| System | `--system` | Git 安装目录下的 `etc/gitconfig` | 当前计算机上的所有用户 |
| Global | `--global` | 用户目录下的 `.gitconfig` | 当前用户的所有仓库 |
| Local | `--local` | 当前仓库的 `.git/config` | 当前仓库 |

配置优先级：

**Local > Global > System**

高优先级配置覆盖低优先级配置，但不会删除低优先级配置。

#### 2.2 查看配置

```cmd
git config --list
git config --list --show-origin
git config --system --list
git config --global --list
git config --local --list
git config --show-origin user.name
```

#### 2.3 设置和删除配置

```cmd
git config --global user.name "用户名"
git config --local user.name "项目用户名"

git config --global --unset user.course
git config --global --unset-all alias.course
```

#### 2.4 多值配置

```cmd
git config --global --add alias.course first
git config --global --add alias.course second

git config --global --get alias.course
git config --global --get-all alias.course
```

- `--add`：添加一个值，不覆盖已有值。
- `--get`：获取一个匹配值，本次实验中返回最后一个值。
- `--get-all`：获取全部匹配值。
- `--unset-all`：删除该配置项的所有值。

#### 2.5 Git 命令别名

设置：

```cmd
git config --global alias.lg "log --oneline --graph --decorate --all"
```

使用：

```cmd
git lg
```

删除：

```cmd
git config --global --unset alias.lg
```

### 3.实验记录

1. 查看了本机的 System、Global、Local 配置。
2. 确认 Global 用户名为 `shi-jinyang`，邮箱为 GitHub noreply 邮箱。
3. 确认 Global HTTP/HTTPS 代理为 `127.0.0.1:7890`。
4. 使用 `user.course` 验证 Local 配置优先于 Global。
5. 删除 Local 测试配置后，Git 自动读取 Global 配置。
6. 删除测试配置，恢复实验环境。
7. 查看了 `%USERPROFILE%\.gitconfig` 的实际内容。
8. 使用 `alias.course` 验证多值配置。
9. 成功创建并使用 `git lg` 别名。

## 2026-11-26：Git 常用高级技巧与工作流总结

### 1.学习目标

掌握 Git 中几种常用的高级命令，理解它们的适用场景，并能够组合使用这些命令完成实际开发任务。

### 2.学习内容

#### 2.1 git stash：临时保存修改

学习了：
- `git stash`：临时保存工作区和暂存区的修改。
- `git stash list`：查看 stash 记录。
- `git stash apply`：恢复修改，但保留 stash 记录。
- `git stash pop`：恢复修改，成功后删除 stash 记录。
- `git stash drop`：删除指定 stash 记录。
- `git stash clear`：清空所有 stash 记录。

实验结果：
- 成功保存未提交的修改。
- 成功恢复文件内容和暂存状态。
- 成功删除 stash 记录。
- 验证了默认情况下普通未跟踪文件不会被 stash 保存。

#### 2.2 git cherry-pick：选择性应用提交

学习了：
- `git cherry-pick <commit>`：将指定提交应用到当前分支。
- `git cherry-pick --continue`：解决冲突后继续操作。
- `git cherry-pick --abort`：取消当前 cherry-pick 操作。
- `git cherry-pick --skip`：跳过当前提交。

实验结果：
- 创建 `main-practice` 和 `feature-practice` 两个分支。
- 成功将 Feature A 的指定提交应用到 main-practice。
- 成功制造并解决 cherry-pick 冲突。
- 最终保留了冲突双方的文件内容。

#### 2.3 git blame：追踪代码修改来源

学习了：
- `git blame <file>`：查看文件每一行最后修改的提交和作者。
- `git blame -L 2,3 <file>`：查看指定行范围。
- `git blame -w`：忽略空白字符变化。
- `git blame -e`：显示作者邮箱。

实验结果：
- 成功追踪 `cherry-demo.txt` 每一行的修改来源。
- 确认不同代码行可以对应不同提交。
- 理解了 blame 显示的是最后修改归属，不一定是最初编写者。

#### 2.4 git bisect：二分查找 Bug

学习了：
- `git bisect start`：开始二分查找。
- `git bisect good`：标记正常版本。
- `git bisect bad`：标记有问题的版本。
- `git bisect reset`：结束查找并返回原分支。
- `git bisect run`：使用自动化脚本判断提交状态。

实验结果：
- 以 `3259750` 为 good，以 `162b4a3` 为 bad。
- 通过模拟判断，最终定位到 `b7e27f8 Add feature A`。
- 成功执行 `git bisect reset`，返回 `main-practice` 分支。

注意：本次 good/bad 判断是教学模拟，并非真实项目 Bug 测试。

### 3.Git 工作流总结

典型功能开发流程：

1. 使用 `git switch -c` 创建功能分支。
2. 修改代码，使用 `git add` 和 `git commit` 保存修改。
3. 需要临时切换任务时使用 `git stash`。
4. 使用 `git merge` 整合分支，或使用 `git cherry-pick` 移植指定提交。
5. 使用 `git blame` 追踪代码修改来源。
6. 使用 `git bisect` 定位引入 Bug 的提交。
7. 使用 `git push` 推送分支，并在 GitHub 上创建 Pull Request。

### 4.本课总结

掌握了 stash、cherry-pick、blame、bisect 四个常用高级命令，并完成了相应实验。
