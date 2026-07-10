---
{"dg-publish":true,"permalink":"/技术文档/版本管理/Git/git命令/","dg-note-properties":{}}
---

# 背景
## tag
标签
- 相当于代码仓库的快照, 只读, 无法在其上进行修改
- 切换到tag (这会使你处于“detached HEAD”状态，即不在任何分支上)
# 常用命令
---
## cherry-pick
- 把指定提交合并到当前分支
- 支持合入多个提交
### 基本格式
- `cherry-pick <commit hsa1>[ <commit hsa2> ...]`
### 参数

---
## commit
### 参数
- `--amend`: 在最新提交的基础上追加提交
---
## rm
- 删除实际文件和索引
### 参数
- `--cached`: 只删除git索引, 不删除实际文件
---
## restore
### 基本格式
- `restore <FILE>`: 删除文件在工作区的改动
### 参数
- ``

---
## tag
列出本地所有tag

---
## format-patch
生成patch文件

---
## rebase
修改提交日志或更改提交内容or换当前分支的基分支
- 参数
	- `-i <target branch | ...>`
		- 指定要修改的提交, 支持批量操作
- 实例
	- 
	- 删除当前分支和目标分支之间的其他分支的提交
		- git rebase -i <目标分支>
			- 把要删除的提交的pick改为drop，保存退出即可
	- 更改之前的某一次提交
		- git rebase -i <commit_id^>
			- 进入nano文本更改pick为edit，保存退出
			- 可选操作
				- 执行git commit --amend可以修改提交信息
			- 此时为变基暂停期间，可以修改当前提交的提交内容，执行命令：git reset HEAD^, 把当前提交的更改重新放入工作区
			- 修改完成后，重新执行add commit等操作
			- git rebase --continue：继续下一个提交
	- 换当前分支的基分支
		- git rebase <目标基分支> <当前分支>

	- -i <commit_id^|HEAD~3...>: 修改当前HEAD为指定提交，并暂存之后的提交

	- --abort：终止变基，回到变基前的状态

	- --continue：继续变基
- 内容解析速查表

|指令|含义（一句话版）|
|---|---|
|`pick <commit>`|应用一个普通提交|
|`reset <label/commit>`|把 HEAD 强制移动到某个点|
|`label <name>`|给当前 HEAD 打一个“临时标签”|
|`merge <label>`|创建一个 merge commit|
|`merge -C <commit> <label>`|用已有 merge 的提交信息来 merge|
|`#`|注释|
|`onto`|rebase 的新基线（不是命令，是 label）|

---
## diff: 查看版本内容差异
- 情况1：都已经提交，工作区没有改动
	- 查看最近两个提交之间的差异
		- `git diff HEAD^ -- <filename>`
	- 查看最近一次提交和上上次提交的差异
		- `git diff HEAD^^ -- <filename>`
	- 以此类推...
- 情况2：工作区改动后，还未执行add命令
	- 查看当前工作区和最近一次提交的版本之间的差别
		- `git diff <filename>`
		- `git diff HEAD -- <filename>`
- 情况3：工作区改动后，执行add命令后但未提交
	- 查看工作区和最近一次提交的版本库之间的区别，比情况2少了一个可执行的命令
		- `git diff HEAD -- <filename>`
- 情况4：生成patch文件
	- `git diff <file> > <patch file>.patch`
---
## config
### 配置级别
- git有三层config文件，分别是系统、全局、本地
	- 记为`LEVEL`, `LEVEL=<local | global | system>`
### 查看配置文件内容
- `git config [--LEVEL] --list`: 查看不同级别配置文件
### 设置/删除变量
- `git config [--LEVEL]  <SECTION.KEY> <VALUE>`: 设置键值，即添加配置项
- `git config [--LEVEL]  --unset <SECTION.KEY>`: 删除配置项
### 常见配置
- `git config [--LEVEL] user.name <name>`: 设置用户名
- `git config [--LEVEL] user.email <email>`：设置邮箱地址
- `git config [--LEVEL] credential.helper <cache | store>`： 创建远程仓库的账号缓存凭证
	- `cache [optionals]`: 在输入一次账号密码之后短时间保存
		- `--timeout=3600`: 设置保存的时间
	- `store`: 永久保存, 默认存储在~/.git-credentials(以明文的形式)
	- 示例
		- `eg. git config --global credential.helper 'cache --timeout=3600'`
		- `eg. git config --local credential.helper 'store'`

- 解除上传文件大小的限制方法

	- git config –global http.postBuffer 1048576000

	- 使用Git LFS（Large File Storage）：Git LFS是一个Git扩展，用于处理大文件。你可以将大文件（例如1GB或更大的文件）存储在Git LFS中，并在git拉取时得到更好的表现。首先，你需要安装并配置Git LFS。通过访问Git LFS官方网站（
---
## remote

- git remote:查看当前仓库的所有远程仓库链接变量名

- git remote show <变量名>:查看当前仓库某个远程仓库链接变量存储数据及相关信息

- git remote add <变量名> <远程仓库地址>:添加远程仓库链接地址到本地仓库的变量中

- git remote delete <变量名>:删除已添加的某个远程仓库地址链接对应的变量名
---
## clone
- `git clone <url> [<options>] [<local_path>]`
	- `<options>`
		- `--single-branch`: 只克隆选择的分支, 不克隆其他分支
		- `-b, --branch <branch_name | tag_name>`: 克隆指定分支/标签到当前目录

---
## submodule
### add
向当前代码仓库中添加子模块
#### 基本格式
`add [options] <target-url | target-path> <local/path>`


**可选参数**
- `-b, --branch`: 指定分支, 也可以后续手动修改`.gitmodules`文件, 参考[[技术文档/版本管理/Git/gitmodules文件\|gitmodules文件]]

### init
根据.gitmodules中的配置初始化子模块
### update
更新为最新的代码库

**示例**
- `git submodule update --init --recursive --force`： 递归的更新拉取子模块, 失败重新拉取
### sync
用于手动修改`.gitmodules`文件内容之后, 同步到当前仓库配置

---
## push

- git push：推送当前分支到上游分支。
- git push --force 或 git push -f：强制推送，覆盖远程分支。
- git push --force-with-lease 或 git push -fwl：安全强制推送，避免覆盖远程分支。
- git push --all 或 git push -a：推送所有本地分支到远程仓库。
- git push --tags：推送所有标签到远程仓库。
- git push --dry-run 或 git push -n：执行非实际推送操作，用于查看将要推送的更改。
- git push --delete 或 git push -d：删除远程分支或标签。
- git push --follow-tags：推送当前分支及其所有相关标签到远程仓库。
- git push --mirror：创建远程仓库的镜像，即推送所有分支、标签和引用。
- git push --prune：移除远程仓库中没有对应本地分支的引用。
- git push --set-upstream, -u origin branch-name：推送本地分支到远程仓库，并设置上游分支。
- git push --progress：显示推送进度。
---
## branch

- git branch -m <old_branch> <new_branch>：修改分支名

- git branch：查看所有分支名以及当前分支

- git branch -d <branch_name>:删除指定分支，删除分支前会检查是否merge，未合并删除失败

- git branch -D <branch_name>:强制删除指定分支

- git branch -u <remote_branch_name>:设置上游分支

- `git branch <branch name>`: 创建分支，但不切换

- git branch -r: 查看远程所有分支

- git branch -a：查看远程和本地所有分支
---
## switch
- `git switch -c <branch name>`: 创建新分支，并切换过去
---
## pull
是一个复合命令，相当于执行了fetch和merge
- `git pull <远程仓库链接变量名> <branch_name>`：从远程仓库指定分支拉取代码到本地当前分支（注意：第一次提交代码到远程仓库前需要拉取一次代码）
- `git pull <远程仓库链接变量名> <branch_name> --allow-unrelated-histories`：允许无关历史的分支合并
---
## stash: 
- `git stash`: 暂存当前更改
- `git stash pop`: 使用暂存的更改
- `git list`
- `git stash drop <number>`
---
## add
- `git add -u`：只把追踪的文件的更改添加到暂存区
- `git add <files>`: 把指定文件或者文件夹添加到暂存区
- `git add` .:标记冲突已解决
---
## checkout
- `git checkout <commit_id>`: 使用指定分支提交的代码
- `git checkout -b <branch_name> [<[origin/]base_branch> | <tag_name>]`: 创建新分支并切换到新分支
	- `<tag_name>`: 基于`tag_name`创建本地下游分支
	- `<[origin/]base_branch>`: 基于某个本地/远程分支创建本地下游分支
- `git checkout [<branch_name> | <tag_name> | <file_path>]`:用最后一次提交覆盖工作区 
	- `<file_path>`:对特定文件执行上述操作, 参考[[技术文档/版本管理/Git/git命令#^46fe47\|#^46fe47]]
	- `<branch_name>`: 切换到指定`branch`
	- `<tag_name>`: 切换到指定`tag`
{ #e302b1}

---
## fetch
- `git fetch <origin> [<branch_name> | tag <tag_name>] [<options>]`
	- `<branch_name>`: 会从远程仓库`origin`的`branch_name`分支拉取最新的更改到本地，但不会自动合并到当前分支
	- `tag <tag_name>`: 把远程仓库`origin`的`tag_name`标签拉取到本地, 可通过`check`命令切换到指定标签, 参考[[技术文档/版本管理/Git/git命令#^e302b1\|#^e302b1]]
	- `<options>`
		- `--tags`: 此命令用于拉取远程仓库所有`tag`到本地, **默认情况下, `fetch`命令是不会拉取`tag`的**
		- `--prune`: 获取远程仓库所欲分支的更新, 并清除以前的缓存
		- `--all`:获取远程仓库所有分支的更新到本地，但不会自动合并这些更新到当前工作分支，它只是更新了本地的远程分支指针
---
## merge

- git merge remote_url/branch_name
---
## reset：一般用来回退版本

- 背景

	- commit_id

		- 可以是一个指定的id

		- 也可以是相对引用, eg. HEAD~3: 表示最近三个提交, 用在回退操作表示回退最近三个提交, 即处于最近第四个提交

- git reset --hard <origin/branch-name>:强制将本地分支的代码重置为远程分支的状态，包括本地分支提交记录（git log），工作区，暂存区都会更新

- git reset --hard <local_commit_id>: 会将指定commit_id之后的提交全部撤回, 并且删除指定commit_id之后提交的提交历史, 工作区，暂存区都会删除

- `git reset --soft <commit>`:更改HEAD指针回到指定的提交，但不会更改暂存区和工作区

- `git reset <commit>`:更改HEAD指针和暂存区，但不会改变工作区
---
# 实例
## 修改之前的提交信息or代码更改，但不会创建新的commit

	- 

## 版本回退相关操作

	- 场景1：如果想将代码恢复到之前某个提交的版本，且那个版本之后提交的版本都不要了

		- 原理：git reset的作用是修改HEAD的位置，即将HEAD指向的位置改变为之前存在的某个版本

		- 操作：

			- git reset --hard <目标版本号>：版本回退到指定版本

			- git push -f：提交更改（注意：-f必不可少，因为本地库的当前版本比远程库要旧，用git push会报错）

	- 场景2：如果我们想撤销之前的某一版本，但是又想保留该目标版本后面的版本，记录下这整个版本变动流程，就可以用这种方法。

		- 原理：我们commit了三个版本（版本一、版本二、 版本三），突然发现版本二不行（如：有bug），想要撤销版本二，但又不想影响撤销版本三的提交，就可以用 git 

		- 操作：

			- git log：查看版本号，找到需要撤销的目标版本号

			- git revert -n <版本号>：重做目标版本

			- git commit -m <提交信息>：提交重做的改动

			- git push：推送到远程库

	- 场景3：commit前

		- 回退所有文件

			- 操作：

				- git reset --hard HEAD

		- 回退单个文件

			- 操作：

				- git checkout <commit-hash> -- <file-path>

	- 场景4：commit后

		- 回退到指定版本但保留工作区

			- 操作

				- git reset --soft <commit-hash>

	- 场景5：push后回退

		- push 进特性分支或自己的独立分支，但没有 merge 进主分支

		- push 后，错误代码已经进入主分支

			- 操作：

				- 修复本地内容

				- 推送至远端

## 恢复误删分支

	- 操作

		- git reflog：列出所有的提交历史，找到被删除分支的最后一次提交的hash值

		- git branch <branch-name> <commit-hash>：恢复指定分支，这个分支名不需要和原来的分支名相同

## 添加代理和删除代理

```
git config --global https.proxy http://127.0.0.1:1080

git config --global https.proxy https://127.0.0.1:1080

git config --global http.https://github.com.proxy http://127.0.0.1:7890

git config --global --unset http.proxy

git config --global --unset https.proxy

npm config delete proxy
```

## 代码合并相关操作

	- API

		- git fetch origin：更新本地远程分支指针指向远程分支的最新状态

		- git merge origin/branch_name：合并远程分支的更新，如果有冲突会提示你手动解决冲突

	- 冲突解决方式

		- 以本地库提交代码到远程库举例

			- 情况1：本地库最近改动的地方和远程库最近改动的地方冲突

				- git pull:先同步远程库的代码到本地，此时会发生冲突

				- vim <filename>: 打开冲突文件解决冲突，并保存

				- git add :标记冲突已解决

				- git commit:提交解决完冲突的版本

				- git push：推送到远程

			- 情况2