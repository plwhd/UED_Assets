# Git 学习

- 分享人：zengqingqing
- 分享日期：2026-03-11
- 教程来源：[廖雪峰的 Git 教程](https://www.liaoxuefeng.com/wiki/)

## 阅读目标

这份笔记用于理解 Git 的基本概念、常用命令、协作场景，以及为什么设计工作流需要进入 Git。

重点不是背命令，而是理解：

- Git 是什么。
- Git 如何记录文件变化。
- 为什么结构化设计资产比图片式设计更适合版本管理。
- 如何通过分支、commit、push 和 PR 完成协作。
- `.git` 目录里大致保存了什么。

## 核心问题

- Git 是什么？
- 为什么使用 Pencil 还原设计稿？
- 为什么将设计工作流搬到 Git？
- 现阶段重点是什么？

## Git 是什么

Git 是分布式版本控制系统，用来记录文件变化、回溯历史版本，并支持多人协作。

集中式版本控制和分布式版本控制的区别：

![集中式](assets/17720043660784.jpg)

![分布式](assets/17720043768539.jpg)

## 为什么使用 Pencil 还原设计稿

版本控制系统更适合管理文本类内容，例如：

- TXT 文件
- HTML / CSS
- 程序代码
- Markdown
- 结构化配置

图片、视频等二进制文件也可以被 Git 管理，但 Git 很难追踪它们内部具体改了什么。系统通常只能记录文件整体变化，例如文件大小从 100KB 变成 120KB。

因此，设计资产有两种不同形态：

- 图片式设计：视觉产物，无法被精确 diff。
- 结构化设计：例如组件化、Token 化、JSON 化，可追踪、可审查、可复用。

## 为什么将设计工作流搬到 Git

把设计搬到 Git，不是为了方便管理文件，而是为了让设计进入工程体系，成为可版本化、可审查、可验证的系统规格。

### 1. 版本管理：让设计变成可追溯资产

Git 能自动记录每一次改动：

- 不需要复制多个文件版本。
- 不需要人工标注“最终版”“最终修改版”。
- 所有改动都天然可回溯。

通过 diff，开发可以看到：

- 哪个组件改了。
- 哪个字段改了。
- 哪个尺寸改了。
- 哪个交互改了。

这对工程协作很友好。

### 2. Figma 文件的常见问题

在 Figma 中，我们通常会遇到：

- 所有内容堆在一个大文件里。
- 文件加载慢。
- 微小改动难以追踪。
- 没有规范化 PR 流程。
- 改动原因缺少说明。
- 组件引用容易混乱。

最终导致设计变更是“感知型”的，而不是“结构型”的。

### 3. Git + PR 强制形成协作记录

Git + PR 可以让设计协作具备工程属性：

- 改动说明
- 审核流程
- 变更记录
- 责任归属
- 可回溯历史

### 4. 设计左移

安全左移（Shift Left Security）是指把安全工作从开发后期前移到开发早期，甚至前移到设计阶段。

“左移”来自软件生命周期：

```text
需求 -> 设计 -> 开发 -> 测试 -> 上线 -> 运维
```

左边代表更早阶段。

当设计变成系统规格的一部分后，设计走查也可以变成类似单元测试的必经环节。这本质上是一种设计左移（Design Shift Left），能够让团队更早发现问题，并降低试错成本。

## 现阶段重点

1. 跑通工作流，用最小成本试错。
2. 达成共识：不改变团队成员职能，只改变协作方式。前端拿到 Pencil 文件，仍然像拿到 Figma 文件一样开始工作。
3. 约定哪些文档是前端可用的，例如 `README.md`。

## 入门练习

### 1. 安装 Git

```bash
brew install git
```

安装后，需要配置 Git 用户名和邮箱。

### 2. 创建版本库

版本库（Repository，简称 Repo）可以理解为一个被 Git 管理的目录。

在这个目录中：

- 所有文件的新增、修改、删除都会被记录。
- 每一次变更都可以追溯。
- 可以在未来任意时间回滚到某个历史版本。

示例仓库路径：

```text
/Users/zengqingqing/workspace/builder
```

### 3. 初始化 Git 仓库

进入目标目录后执行：

```bash
git init
```

初始化后，目录中会生成隐藏文件夹 `.git`。它是 Git 用来记录版本信息的核心目录。

不要手动修改 `.git` 里的内容，否则可能会破坏仓库。

查看隐藏文件：

```bash
ls -ah
```

### 4. 添加并提交文件

新建 `readme.txt`，写入：

```text
Git is a version control system.
Git is free software.
```

添加到暂存区：

```bash
git add readme.txt
```

提交到仓库：

```bash
git commit -m "wrote a readme file"
```

示例输出：

```text
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

`-m` 后面的内容是本次提交说明，用来帮助我们从历史记录中找到改动。

### 5. 查看状态和差异

查看当前状态：

```bash
git status
```

查看某个文件的修改内容：

```bash
git diff readme.txt
```

常见流程：

```bash
git status
git add .
git commit -m "xxxxx"
git status
```

每一次 commit，都是一次可回溯的版本记录。

### 6. 版本回退练习

修改 `readme.txt`：

```text
Git is a distributed version control system.
Git is free software.
```

查看状态：

```bash
git status
```

示例输出：

```text
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

查看差异：

```bash
git diff readme.txt
```

示例输出：

```diff
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
```

添加修改：

```bash
git add readme.txt
```

确认暂存区：

```bash
git status
```

提交：

```bash
git commit -m "add distributed"
```

提交后查看状态：

```bash
git status
```

如果显示下面内容，说明工作区已经干净：

```text
nothing to commit, working tree clean
```

查看提交日志：

```bash
git log
```

## 核心场景速查

### 1. 开启新任务

```bash
git checkout next-ui
git pull upstream next-ui
git checkout -b feat-xxx
```

### 2. 提交改动

```bash
git add .
git commit -m "..."
```

### 3. 更新 PR

```bash
git push origin HEAD
```

这会把当前分支推送到远程同名分支，具体目标取决于当前配置的 `origin`。

### 4. PR 冲突或同步

```bash
git fetch upstream
git rebase upstream/next-ui
git push origin HEAD -f
```

### 5. 任务完成后清理

```bash
git checkout next-ui
git reset --hard upstream/next-ui
```

## 工作场景

### 场景一：提交文件夹到 Git

需求：`~/workspace/h` 中有两个文件夹 `a` 和 `b`，需要提交到 Git。

#### 第一步：进入仓库

```bash
cd ~/workspace/h
```

确认当前目录是 Git 仓库：

```bash
ls -a
```

必须能看到：

```text
.git
```

#### 第二步：查看当前状态

```bash
git status
```

如果 `a` 和 `b` 还没有被 Git 管理，会看到：

```text
Untracked files:
  a/
  b/
```

#### 第三步：添加到暂存区

一次性提交全部内容：

```bash
git add .
```

只提交 `a` 和 `b`：

```bash
git add a b
```

#### 第四步：确认已进入暂存区

```bash
git status
```

应该看到：

```text
Changes to be committed:
  new file: a/xxx
  new file: b/xxx
```

#### 第五步：提交

```bash
git commit -m "add folders a and b"
```

#### 第六步：推到 GitHub

先确认远程仓库：

```bash
git remote -v
```

如果已经连接远程仓库：

```bash
git push origin main
```

### 场景二：Review PR

不需要先切换到跟踪分支 `upstream/ui`。

拉取 PR 内容：

```bash
git fetch upstream pull/2890/head:pr_2890
```

说明：

- `2890` 是 PR 编号。
- `pr_2890` 是用于 review 的本地分支名。

切换到新建分支：

```bash
git checkout pr_2890
```

### 场景三：保存 Review 修改并同步到远端

在 `pr_2890` 的基础上修改，并同步到对应 PR。

#### 第一步：提交到本地仓库

```bash
git add .
git commit -m "您的提交信息描述"
```

数据流：

```text
工作区 (Working Directory)
    ↓ git add .
暂存区 (Staging Area)
    ↓ git commit
本地仓库 (Local Repository)
    ↓ git push
远程仓库 (Remote Repository)
```

#### 第二步：推送到远程仓库

常见远程配置：

```text
origin:   您的 fork，例如 qingqing-ux/builder
upstream: 原始仓库，例如 goplus/builder
```

推送到自己的 fork：

```bash
git push origin pr_2890
```

然后在 GitHub 上创建 Pull Request：

```text
from: qingqing-ux/builder:pr_2929
to:   goplus/builder:dev
```

### 场景四：在电脑初始化 Git 仓库

进入工作区：

```bash
cd /Users/zengqingqing/workspace/
```

创建文件夹：

```bash
mkdir test
```

`mkdir` 是 make directory 的缩写，表示创建目录。

创建 Markdown 文件：

```bash
touch test.md
```

创建并写入内容：

```bash
echo "# 标题" > test.md
```

说明：

- `echo`：输出内容。
- `>`：将输出重定向到文件。
- `test.md`：目标文件名。

打印当前工作目录：

```bash
pwd
```

进入项目目录：

```bash
cd /Users/zengqingqing/workspace/<文件夹名称>
ls
```

初始化仓库：

```bash
git init
```

成功后，`git status` 会显示当前仓库状态，并生成 `.git` 目录。

在 Finder 中显示隐藏文件：

```text
Command + Shift + .
```

### 场景五：通过 `.git` 文件变化理解数据结构

练习路径：

1. 进入工作区。
2. 初始化 Git 仓库。
3. 建立 `a.md` 文件，观察 hash 变化。
4. 建立文件夹 `b`，并在其中放入 `a.md`，观察 refs 和 HEAD 变化。
5. 尝试更改 hash，理解内容替换。
6. 使用 `git cat-file -p` 查看对象内容。

Git 有三种核心对象类型：

- `commit`
- `tree`
- `blob`

`git commit` 会记录：

- tree
- 父 commit
- author
- commit message

### 场景六：远程协作

在 `qingqing-ux` 账号下 fork `goplus/builder` 仓库的 `ui` 分支。

查看远程仓库地址：

```bash
git remote -v
```

常见远程关系：

```text
origin   git@github.com:qingqing-ux/builder.git
upstream https://github.com/goplus/builder.git
```

说明：

- `origin`：自己的 fork。
- `upstream`：原始仓库。

#### 同步 upstream 的 ui 分支

切换到 `ui` 分支：

```bash
git checkout ui
```

从 upstream 拉取最新更改：

```bash
git fetch upstream
```

将 `upstream/ui` 合并到本地 `ui` 分支：

```bash
git merge upstream/ui
```

其他合并示例：

```bash
git merge upstream/dev
git merge origin/dev
git merge dev
```

推送到自己的 origin 仓库：

```bash
git push origin ui
```

#### 从 origin 创建 PR 到 upstream

确保当前分支已推送到 origin：

```bash
git push origin paper-test
```

`paper-test` 是当前所在的 Git 分支名称。

创建 PR：

```bash
gh pr create --repo goplus/builder --base ui --head qingqing-ux:paper-test
```

说明：

- `gh pr create`：创建 Pull Request。
- `--repo goplus/builder`：指定 PR 要合并到哪个仓库。
- `--base ui`：指定目标分支。
- `--head qingqing-ux:paper-test`：指定源分支。

### 场景七：新建并切换分支

Git 分支名不能包含空格，建议使用连字符连接。

```bash
git checkout -b design-style-modification
```

### 场景八：将一个分支合并到另一个分支

示例关系：

```text
ui 分支跟踪 origin/ui
HEAD -> ui, upstream/ui, origin/ui
```

如果 `sprite-ui` 的改动需要提交到 `origin/ui`：

```bash
git switch ui
git merge --ff-only sprite-ui
git push origin ui
```

### 场景九：文件防丢失

新文件防丢失：

```bash
git add .
git commit -m "init"
```

已跟踪文件防丢失：

```bash
git commit -am "wip"
```

## Git 概念速查

### Git 是内容寻址数据库

Git 中所有文件内容都作为对象保存，并通过哈希值组织。

核心对象：

- `commit`：提交记录。
- `tree`：目录结构。
- `blob`：文件内容。

Git 依靠 commit、tree、blob 和引用关系组织版本历史。

### 常用命令

```bash
git add .
git commit -m "xxxxx"
git status
git fetch
git push
git pull
```

命令含义：

- `git fetch`：下载远程更新，但不自动合并。
- `git push`：上传本地提交到远程。
- `git pull`：下载远程更新并尝试合并到当前分支。

### Git 的三个区域

```text
工作区 (Working Directory)
        ↓ git add
暂存区 (Staging Area)
        ↓ git commit
版本库 (Repository)
```

### 查看 Git 对象内容

```bash
git cat-file -p <commit-hash>
```

## `.git` 目录

### `.git/HEAD`

查看当前指针：

```bash
cat .git/HEAD
```

示例：

```text
ref: refs/heads/main
```

表示当前正在 `main` 分支上工作。

### `.git/objects`

`.git/objects` 保存 Git 的核心对象，包括：

- `blob`
- `tree`
- `commit`

练习：

```bash
touch a.txt
git add .
git commit -m "first"
```

Git 会：

1. 创建 blob，保存 `a.txt` 的内容。
2. 创建 tree，保存当前目录结构。
3. 创建 commit，记录作者、时间和指向的 tree。
4. 将对象存入 `.git/objects`。

### `.git/refs`

`.git/refs` 保存分支和标签。

例如：

```text
.git/refs/heads/main
```

这个文件记录 `main` 分支当前指向哪个 commit。
