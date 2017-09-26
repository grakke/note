# 代码托管

- [GitHub](https://github.com/)
- [Bitbucket](https://bitbucket.org/product)
- [Gitlab](https://github.com/)
- [开源中国](https://github.com/)
- [Coding](https://github.com/)

## Install:

```
sudo apt-get install git
brew install git
```

## Config:

git clone有两种方式https与ssh，SSH keys的使用需保证remote的源为git方式

- 全局配置：/etc/gitconfig文件 `git config --system` 
- 用户配置：home目录下的 .gitconfig文件 `git config --global` 
- 项目配置：项目目录下.git/config文件 `git config `
- 查看配置:`git config --list --show-origin`

### key生成

#### SSH
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
#### GPG
提交内容将会有一个“已验证”标记
```
gpg --gen-key
gpg --list-secret-keys --keyid-format LONG  //获取GPG key ID  3AA5C34371567BD2
gpg --list-key
sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
gpg --armor --export 3AA5C34371567BD2  // get the key,add to github
git config --global user.signingkey 35F5FFB2
```
### 用户信息配置
```
git config --global user.name "name"
git config --global user.email "email"
git config --global color.ui "auto"
```

### 个性化配置

理解每个指令的原理

```
[user]
email = liboming88@yeah.net
name = Henryli

[alias]  // .gitconfig中添加alias
prune = fetch --prune
# Because I constantly forget how to do this
# https://git-scm.com/docs/git-fetch#git-fetch--p

undo = reset --soft HEAD^
# Not quite as common as an amend, but still common
# https://git-scm.com/docs/git-reset#git-reset-emgitresetemltmodegtltcommitgt

stash-all = stash save --include-untracked
# We wanna grab those pesky un-added files!
# https://git-scm.com/docs/git-stash

glog = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'
# No need for a GUI - a nice, colorful, graphical representation
# https://git-scm.com/docs/git-log
# via https://medium.com/@payload.dd/thanks-for-the-git-st-i-will-use-this-4da5839a21a4

[merge]
ff = only
# I pretty much never mean to do a real merge, since I use a rebase workflow.
# Note: this global option applies to all merges, including those done during a git pull
# https://git-scm.com/docs/git-config#git-config-mergeff

conflictstyle = diff3
# Standard diff is two sets of final changes. This introduces the original text before each side's changes.
# https://git-scm.com/docs/git-config#git-config-mergeconflictStyle

[commit]
gpgSign = true
# "other people can trust that the changes you've made really were made by you"
# https://help.github.com/articles/about-gpg/
# https://git-scm.com/docs/git-config#git-config-commitgpgSign

[push]
default = simple
# "push the current branch back to the branch whose changes are usually integrated into the current branch"
# "refuse to push if the upstream branch’s name is different from the local one"
# https://git-scm.com/docs/git-config#git-config-pushdefault

followTags = true
# Because I get sick of telling git to do it manually
# https://git-scm.com/docs/git-config#git-config-pushfollowTags

[status]
showUntrackedFiles = all
# Sometimes a newly-added folder, since it's only one line in git status, can slip under the radar.
# https://git-scm.com/docs/git-config#git-config-statusshowUntrackedFiles

[transfer]
fsckobjects = true
# To combat repository corruption!
# Note: this global option applies during receive and transmit
# https://git-scm.com/docs/git-config#git-config-transferfsckObjects
# via https://groups.google.com/forum/#!topic/binary-transparency/f-BI4o8HZW0

# A nice little github-like colorful, split diff right in the console.
# via http://owen.cymru/github-style-diff-in-terminal-with-icdiff/
[diff]
tool = icdiff
[difftool]
prompt = false
[difftool "icdiff"]
cmd = /usr/local/bin/icdiff --line-numbers $LOCAL $REMOTE
```

#### alias说明

- prune = fetch --prune - 当在其他人将分支推送到远程仓库时，我也会得到了大量的本地分支。Prune可以删除远端已经删除的任何本地分支。
- undo = reset --soft HEAD ^ - 如果我在做出提交时犯了一个错误，这个命令会把代码恢复到提交之前的样子。通常我只是在这种情况下修改现有的提交，因为它保留了提交信息。
- stash-all = stash save --include-untracked - 当你正在开发，有人临时要求你切换分支时，stash 是非常有用的。这个命令确保当你 stash 时，可以记录没有被 git add 的新文件。
- merge
  + ff = only 确保只有在每一个合并都是 fast-forward 的时候，你才会看到报错。否则只要你配置了这个选项，什么合并提交，什么历史记录，通通都不需要，只是两次提交之间的平滑过渡。你可能会想知道如何完成这项工作。答案是用 git rebase，把一个分支的修改合并到当前分支，它非常有用当我 pull 代码与 master 有冲突的时候，我使用这种方式来处理。当你在本地分支上修改后，同时其他人在 master 上 做了修改，我想这样比你直接 merge 到你本地分支时的 commit 更好。这样你可以避免多出一个 merge 的 commit。如果我打算新建一个merge commit，我可以用明确的 git merge -ff 来创建。
- commit
  + gpgSign = true 确保您的所有 commit 都由你的 GPG 密钥签名。这通常是一个好主意，因为 .gitconfig 文件中没有验证您的用户信息，这意味着看起来像您这样的提交可能会轻松显示在其他人的提交 信息中。事实上，我曾经用过别人的凭据，因为帐户和机器配置耗时太长。我的提交请求是通过别人的帐号提交的，但内部的所有提交都是我的真实账号。将你的 GPG key 添加到 Github并尝试一次提交，你可能就会解决你现在的疑问，您提交内容将会有一个“已验证”标记。
  - 如果您有多个 GPG 密钥，可以使用 user.signingKey 选项指定要使用的密钥。
  - 上述的配置在 GUI 工具里不会生效，你需要在工具里的设置里找配置项。
  - gpg-agent可以保存口令，让我们更方便。
- Push
  + default = simple可能是你已经设置的配置项。它可以更轻松地将您的本地分支推送到远程，当二者分支名一样的时候。
  + followTags = true很简单。配置它以后，当你 git push 的时候可以直接将本地的 tags 提交到远程，而不用每次都加参数 --follow-tags。不知道你是不是和我一样，我如果创建了一个tag，我就基本上一定会将它推到远程的。

Git 命令清单
![](../_static/bg2015120901.png)
![](../_static/git_2.png)

## 原理

- 工作区（当前文件状态Workspace）进行开发改动的地方，任何对象都是在工作区中诞生和被修改；
- 暂存区（提交最新的版本Index / Stage）.git目录下的index文件, 暂存区会记录git add添加文件的相关信息(文件名、大小、timestamp...)，不保存文件实体, 通过id指向每个文件实体。任何修改都是从进入index区才开始被版本控制；
- 版本库 本地仓库（所有历史版本Repository）保存了对象被提交 过的各个版本，只有把修改提交到本地仓库，该修改才能在仓库中留下痕迹；
- 远程仓库(Remote)
- 任何对象都是在工作区中诞生和被修改；
- 任何修改都是从进入index区才开始被版本控制；
- 只有把修改提交到本地仓库，该修改才能在仓库中留下痕迹；
- 与协作者分享本地的修改，可以把它们push到远程仓库来共享。

### 文件三种状态：modified staged committed:

Git 的工作就是创建和保存项目的快照及与之后的快照进行对比

### 创建版本库

- git init：在当前目录新建一个Git代码库
- git init [project-name] :# 新建一个目录，将其初始化为Git代码库
- git clone [url] [project-name]:下载一个项目和它的整个代码历史

### 编辑项目:提交到暂存区

```
git add ./<file1>(<file2> <file3>)/[dir] （所有修改过的文件/单个文件 或通过使用通配符将一组文件添加到暂存区）
git add -p 添加每个变化前，都会要求确认,对于同一个文件的多处变化，可以实现分次提交
git rm [file1] [file2] ... 删除工作区文件，并且将这次删除放入暂存区
git rm --cached [file]  停止追踪指定文件，但该文件会保留在工作区
git mv [file-original] [file-renamed]  改名文件，并且将这个改名放入暂存区

git commit -m "the first commit"：提交修改
git commit [file1] [file2] ... -m [message]
git commit -a:提交工作区自上次commit之后的变化，直接到仓库区,通过编辑器添加message
git commit -v：提交时显示所有diff信息
git commit –-am/--amend -m [message]：使用一次新的commit，替代上一次提交,如果代码没有任何新变化，则用来改写上一次commit的提交信息
git commit --amend [file1] [file2] ...  重做上一次commit，并包括指定文件的新变化
git pull --rebase origin master:获取最新远程分支并合并
```

暂存区编辑:

```
git checkout [file]  恢复暂存区的指定文件到工作区
git checkout [commit] [file] 恢复某个commit的指定文件到暂存区和工作区
git checkout . 恢复暂存区的所有文件到工作区
git checkout  branchname/ remotes/origin/branchname  / 158e4ef8409a7f115250309e1234567a44341404 / HEAD
git reset [file] 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
git reset --hard 重置暂存区与工作区，与上一次commit保持一致
git reset [commit] 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
git reset --hard [commit] 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
git reset --keep [commit] 重置当前HEAD为指定commit，但保持暂存区和工作区不变
git revert [commit] 新建一个commit，用来撤销指定commit,后者的所有变化都将被前者抵消，并且应用到当前分支
git stash - 将尚未完成需要保存的工作暂存到stash 中
git stash list - 查看stash中有哪些内容
git stash apply - 恢复stash内容到工作区，但是并不删除stash中的内容
git stash drop - 删除stash中的内容
git stash pop - 恢复stash内容到工作区，并删除stash中的内容

git pull                         # 抓取远程仓库所有分支更新并合并到本地
git pull --no-ff                 # 抓取远程仓库所有分支更新并合并到本地，不要快进合并
git fetch origin     git merge origin/master             # 抓取远程仓库更新   将远程主分支合并到本地当前分支 等同于git pull
git checkout --track origin/branch     # 跟踪某个远程分支创建相应的本地分支
git checkout -b <local_branch> origin/<remote_branch>  # 基于远程分支创建本地分支，功能同上

git reset --hard:回滚到最后一次推送状态
git checkout ./file:回滚最新版本库文件，抛弃工作区修改
git reset HEAD:拉回历史版本
rebase:将本次修改起始的远程仓库节点之后的修改内容优先合并到本地修改分支上
conflict：git rebase出现冲突，修改冲突文件，每次修改,只修改自己添加的内容，每次不需commit，最后git push -f提交到远程仓库
git add file
git rebase --continue
```

查看：

```
git stutus:工作树与暂存区的文件对比差别,显示有变更的文件
git show [$id]:显示某次提交的内容
git diff :查看执行 git status 的结果的详细信息
git diff --staged:暂存区与最新一次提交之间的差别
git diff HEAD:本次提交与上次提交之间的区别
git log --oneline  --graph --reverse  --author=Linus --oneline -5  -before={3.weeks.ago} --after={2010-04-18} --no-merges:显示当前分支的版本历史
git log --graph --pretty=oneline --abbrev-commit （仅展示commit信息的图形化分支）
git log --stat 显示commit历史，以及每次commit发生变更的文件
git log -S [keyword] 搜索提交历史，根据关键词
git log [tag] HEAD --pretty=format:%s  显示某个commit之后的所有变动，每个commit占据一行
git log [tag] HEAD --grep feature 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
git log --follow [file] 显示某个文件的版本历史，包括文件改名
git whatchanged [file] 显示某个文件的版本历史，包括文件改名
git log -p [file] 显示指定文件相关的每一次diff
git log -5 --pretty --oneline 显示过去5次提交
git shortlog -sn 显示所有提交过的用户，按提交次数排序
git blame [file] 显示指定文件是什么人在什么时间修改过
git diff 显示暂存区和工作区的差异
git diff --cached [file] 显示暂存区和上一个commit的差异
git diff HEAD 显示工作区与当前分支最新commit之间的差异
git diff [first-branch]...[second-branch] 显示两次提交之间的差异
git diff --shortstat "@{0 day ago}" 显示今天你写了多少行代码
git show [commit] 显示某次提交的元数据和内容变化
git show --name-only [commit] 显示某次提交发生变化的文件
git show [commit]:[filename] 显示某次提交时，某个文件的内容
git reflog 显示当前分支的最近几次提交

git log -3
git log --since=yesterday
git blame filename:查看文件中每行的操作时间
HEAD：最后一次提交,HEAD^^:前两次提交 HEAD~3：前三次提交
```

分支：

```
git branch [-r]/[-a] 列出所有本地分支/远程/所有
git branch [branch-name] [commit] 新建一个分支，指向指定commit,但依然停留在当前分支
git branch -b new from:通过from创建new分支，并切换到new分支
git branch --track [branch] [remote-branch] 新建一个分支，与指定的远程分支建立追踪关系
git checkout -b branch-name origin/branch-name 从本地创建和远程对应的分支

git checkout dev:切换
git checkout -:切换到上一个分支
git merge new 合并指定分支到当前分支
git cherry-pick [commit] 选择一个commit，合并进当前分支
git branch -d [branch-name] 删除分支
git rebase source destiantion：将source压缩到destiantion
git rebase master
git branch --set-upstream-to=origin/master master
```

标签

```
git tag:列出所有tag
git tag [tag] :新建一个tag在指定commit
git tag -d [tag] 删除本地tag
git push origin :refs/tags/[tagName] :删除远程tag
git show [tag]:查看tag信息
git push [remote] [tag]:提交指定tag
git push [remote] --tags:提交所有tag
git checkout -b [branch] [tag]:新建一个分支，指向某个tag
```

远程分支：

```
git fetch [remote] 下载远程仓库的所有变动
git remote -v 显示所有远程仓库
git remote show [remote] 显示某个远程仓库的信息
git remote add [shortname] [url] 增加一个新的远程仓库，并命名
git pull [remote] [branch] 取回远程仓库的变化，并与本地分支合并
git push [remote] [branch] 上传本地指定分支到远程仓库. git push origin my:master
git push [remote] --force 强行推送当前分支到远程仓库，即使有冲突
git push [remote] --all 推送所有分支到远程仓库
git push origin branch-name 从本地推送分支

git remote -v:每个别名的实际链接地址
git remote show origin           # 查看远程服务器仓库状态
git remote add [shortname] [url] 添加
git remote set-url origin git@github.com:whuhacker/Unblock-Youku-Firefox.git # 设置远程仓库地址(用于修改远程仓库地址)
git push <remote repository name> <branch name>（第一次 git push -u：-u 选项设置本地分支去跟踪远程对应的分支）
git push <remote name> <local branch name:remote branch name>
git branch -dr [remote/branch] :删除远程分支
git push origin --delete dev :删除远程分支
git push                         # push所有分支
git push origin master           # 将本地主分支推到远程主分支
git push -u origin master        # 将本地主分支推到远程(如无远程主分支则创建，用于初始化远程仓库)
git push origin <local_branch>   # 创建远程分支， origin是远程仓库名
git push origin <local_branch>:<remote_branch>  # 创建远程分支
git push origin :<remote_branch>  #先删除本地分支(git branch -d <branch>)，然后再push删除远程分支
```

打包:

```
git archive
```

设置跟踪远程库和本地库：

```
git branch --set-upstream master origin/master 建立追踪关系，在现有分支与指定的远程分支之间
git branch --set-upstream develop origin/develop
```

# 搭建git服务器

- groupadd git adduser git -g git
- 创建证书 mkdir -p ~/.ssh chmod 700 .ssh touch .ssh/authorized_keys chmod 600 .ssh/authorized_keys
- 将客户端的id_rsa.pub文件，把导入到服务器端/home/git/.ssh/authorized_keys
- 新建仓库 mkdir ~/gitrepo chown git:git gitrepo/ cd gitrepo git init --bare runoob.gitsudo git init --bare /path/to/repo.git sudo chown -R git:git sample.git
- 禁止git用户登录shell:修改/etc/passwd 为git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell git:x:503:503::/home/git:/sbin/nologin
- git clone git@server:/path/to/repo.git

## 工作流：

- **1.集中式工作流**：维护一个master分支，开发者提交自己功能修改到中央库前，需要先fetch在中央库的新增提交，rebase自己提交到中央库提交历史之上.

  ```
   git pull --rebase origin master
  ```

- **2.功能性分支**：所有的功能开发应该在一个专门的分支，而不是在master分支上。功能开发隔离也让pull requests工作流成功可能， pull requests工作流能为每个分支发起一个讨论，在分支合入正式项目之前，给其它开发者有表示赞同的机会。

  - 开发者每次在开始新功能前先创建一个新分支。 功能分支应该有个有描述性的名字，比如animated-menu-items或issue-#1061，隔离功能的开发。 `git checkout -b animated-menu-items master`
  - 功能分支也可以（且应该）push到中央仓库中 `git push -u origin animated-menu-items`
  - 合并：push到中央仓库的功能分支上并发起一个Pull Request请求去合并修改到master。Code Review

    ```
      git checkout master
      git pull
      git pull origin animated-menu-items(合并分支)
      git push
    ```

- **3.Gitflow工作流**：通过为功能开发、发布准备和维护分配独立的分支，让发布迭代过程更流畅。![](https://github.com/xirong/my-git/raw/master/images/git-workflow-release-cycle-4maintenance.png)

  - 分支：

    - develop分支作为功能的集成分支，包含了项目的全部历史。

      ```
        git branch develop
        git push -u origin develop
      ```

    - 功能分支（feature）：使用develop分支作为父分支。当新功能完成时，合并回develop分支。

      ```
        git checkout -b some-feature develop
        git pull origin develop
        git checkout develop
        git merge some-feature
        git push
        git branch -d some-feature
      ```

    - 发布分支（release）：清理发布、执行所有测试、更新文档和其它为下个发布做准备操作的地方，像是一个专门用于改善发布的功能分支。只要创建这个分支并push到中央仓库，这个发布就是功能冻结的。任何不在develop分支中的新功能都推到下个发布循环中（自动化脚本执行）。

      ```
        git checkout -b release-0.1 develop
      ```

    - master分支存储了正式发布的历史：合并修改到master分支和develop分支上，删除发布分支。

      ```
        git checkout master（功能回归分支）
        git merge release-0.1
        git push
        git checkout develop
        git merge release-0.1
        git push
        git branch -d release-0.1
        git tag -a 0.1 -m "Initial public release" master（打好Tag以方便跟踪）
        git push --tags
      ```

    - 维护分支：生成快速给产品发布版本（production releases）打补丁，这是唯一可以直接从master分支fork出来的分支。 修复完成，修改应该马上合并回master分支和develop分支（当前的发布分支），master分支应该用新的版本号打好Tag。

      ```
        git checkout -b issue-#001 master
        # Fix the bug
        git checkout master
        git merge issue-#001
        git push
        git checkout develop（重要修改需要包含到develop分支）
        git merge issue-#001
        git push
        git branch -d issue-#001
      ```

  - 流程：develop分支上有了做一次发布（或者说快到了既定的发布日）的足够功能，就从develop分支上checkout一个发布分支。 新建的分支用于开始发布循环，所以从这个时间点开始之后新的功能不能再加到这个分支上---- 这个分支只应该做Bug修复、文档生成和其它面向发布任务。 一旦对外发布的工作都完成了，发布分支合并到master分支并分配一个版本号打好Tag。 另外，这些从新建发布分支以来的做的修改要合并回develop分支

  - 利用Git有提供各种勾子（hook），即仓库有事件发生时触发执行的脚本。 可以配置一个勾子，在你push中央仓库的master分支时，自动构建好对外发布。

- **4.Forking工作流**

让各个开发者都有一个服务端仓库。这意味着各个代码贡献者有2个Git仓库而不是1个：一个本地私有的（fork，其它开发者不允许push到这个仓库，但可以pull到修改。为了方便和其它的开发者共享分支。 各个开发者应该用分支隔离各个功能，就像在功能分支工作流和Gitflow工作流一样。），另一个服务端公开的（公开的正式仓库存储在服务器上，**让正式仓库之所以正式的唯一原因是它是项目维护者的公开仓库**）

```
- 优点：贡献的代码可以被集成，而不需要所有人都能push代码到仅有的中央仓库中。 开发者push到自己的服务端仓库，而只有项目维护者才能push到正式仓库。 这样项目维护者可以接受任何开发者的提交，但无需给他正式代码库的写权限。

- fork操作基本上就只是一个服务端的克隆，clone到本地

- 需要2个远程别名 —— 一个指向正式仓库，另一个指向开发者自己的服务端仓库。别名的名字可以任意命名，常见的约定是使用origin作为远程克隆的仓库的别名 （这个别名会在运行git clone自动创建），upstream（上游）作为正式仓库的别名。

        git remote add upstream https://user@bitbucket.org/maintainer/repo.git

- 功能修改提交到自己仓库中，跟随正式仓库，pull快进合并

        git checkout -b some-feature
        # Edit some code
        git commit -a -m "Add first draft of some feature"
        git pull upstream master（开发者和正式仓库做同步）
        git push origin feature-branch
        # pull requests（简单的通知，而是为讨论提交的功能的一个专门论坛）
- 项目维护者：第一种,直接在pull request中查看代码；第二种，pull代码到他自己的本地仓库，再手动合并。

        git fetch https://bitbucket.org/user/repo feature-branch
        # 查看变更
        git checkout master
        git merge FETCH_HEAD
```

- 解析Pull Request：当要发起一个Pull Request，你所要做的就是请求（Request）另一个开发者（比如项目的维护者） 来pull你仓库中一个分支到他的仓库中。这意味着你要提供4个信息以发起Pull Request： 源仓库、源分支、目的仓库、目的分支。

  - Code Review

# 实际场景

使用 Git 作为版本控制软件最看重的还是结合公司自己搭建的 Gitlab，将 Code Review 加入打包部署持续集成的流程中，这样，代码开发完成，提交测试前，便可以对开发人员提交的代码进行 Review，发现潜在的问题，及时指导，对于新人来讲，也能更快更好的学习。

- 能支持日常迭代开发、紧急线上bug修复、多功能并行开发
- 大概50人左右的团队，平日迭代项目较多，且周期短（1~2周一个迭代）
- 能够通过tag重建整个系统
- 支持code review
- 所有上线的代码必须都是经过测试保证，且能自动同步到下一次的迭代中
- 能和公司的项目管理/持续集成系统整合

下面为团队在日常开发中总结出来的适合企业开发的模式，下面进行简单的介绍，方便大家学习了解（本模式适合敏捷开发流程，小迭代上线，传统的瀑布开发模型并没有进行测试）![](https://github.com/xirong/my-git/raw/master/images/branch_module.png)

- 迭代需求会、冲刺会后确定本次迭代的目标后，将迭代内容视为一个项目，在 Gitlab 上创建一个 Repository，初始化工程代码结构，根据上线日期，比如20150730上线，开出分支 release20150730、dev20150730 两个分支，dev 分支作为日常开发主干分支，release 分支作为提测打包、Code Review 的分支。 -
- 迭代开始，日常开发进行中，开发人员在 dev 分支上进行 Commit、Push 代码，并且解决掉日常协同开发中的冲突等问题，等到达到提测条件的时候，提测者，首先 Merge Master 分支上的最新代码 git merge --no-ff origin/master ，使得 Master 分支上的变更更新到迭代开发分支dev上面，之后，在 Gitlab 上面发起 pull request 请求，并指定 Code Review 人，请求的分支选择本次上线的 release 分支，即 release20150730。

- 被指定 Code Review 的人，对发起者的代码 Review 后，决定是否可以提交测试，若有问题，评论注释代码后，提交者对代码进行进行修改，重复步骤2，直到代码 Review 者认为 Ok。之后便可以借助自己公司的打包部署，对这些代码发布到测试环境验证。

- 步骤2-3重复多次后，就会达到一个稳定可发布的版本，即上线版本，上线后，将 release 版本上面最后的提交（图中0.2.4上线对应处）合并到 Master 分支上面，并打 Tag0.3。至此，一次完整的迭代开发完成。

- 若此次上线后，不久发现生产环境有 Bug 需要修复，则从 Tag 处新开分支 release_bugfix_20150731、dev_bugfix_20150731 ，开发人员从 dev_bugfix_20150731分支上进行开发，提测code review在 release_bugfix_20150731 分支上，具体步骤参考2-3，测试环境验证通过后，发布到线上，验证OK，合并到 Master 分支，并打 Tag0.2.3，此次 Bug 修复完毕，专为解 Bug 而生的这两个分支可以退伍了，删除release_bugfix_20150731、dev_bugfix_20150731两分支即可。（所有的历史 Commit 信息均已经提交到了 Master 分支上，不用担心丢失）

- master：master永远是线上代码，最稳定的分支，存放的是随时可供在生产环境中部署的代码，当开发活动告一段落，产生了一份新的可供部署的代码时，发布成功之后，代码才会由 aone2 提交到 master，master 分支上的代码会被更新。应用上 aone2 后禁掉所有人的 master的写权限

- develop：保存当前最新开发成果的分支。通常这个分支上的代码也是可进行每日夜间发布的代码，只对开发负责人开放develop权限。 -

- feature: 功能特性分支，每个功能特性一个 feature/ 分支，开发完成自测通过后合并入 develop 分支。可以从 master 或者develop 中拉出来。 - hotfix: 紧急bug分支修复分支。修复上线后，可以直接合并入master。

# Git-Develop 分支模式：

是基于 Git 代码库设计的一种需要严格控制发布质量和发布节奏的开发模式。develop 作为固定的持续集成和发布分支，并且分支上的代码必须经过 CodeReview 后才可以提交到 Develop 分支。它的基本流程如下：

![](https://github.com/xirong/my-git/raw/master/_image/2016-09-22-20-57-27.jpg)

- 每一个需求/变更都单独从Master上创建一条Branch分支；
- 用户在这个Branch分支上进行Codeing活动；
- 代码达到发布准入条件后aone上提交Codereview，Codereview通过后代码自动合并到- Develop分支；
- 待所有计划发布的变更分支代码都合并到Develop后，系统再 rebase master 代码到Develop 分支，然后自行构建，打包，部署等动作。
- 应用发布成功后Aone会基于Develop分支的发布版本打一个"当前线上版本Tag"基线；
- 应用发布成功后Aone会自动把Develop分支的发布版本合并回master；

# 问题列表Issues

# GitHub

GitHub集成其他功能：`repository > Settings > Integrations & services`

![Git 使用规范流程](..\_static\bg2015080501.png)

```
# 获取主干最新代码
git checkout master
git pull

# 新建一个开发分支myfeature
git checkout -b myfeature

# 提交分支commit
git add --all
$ git status
$ git commit --verbose

commit:第一行是不超过50个字的提要，然后空一行，罗列出改动原因、主要变动、以及需要注意的问题。最后，提供对应的网址（比如Bug ticket）。
Present-tense summary under 50 characters

* More information about commit (under 72 characters).
* More information about commit (under 72 characters).

http://project.management-system.com/ticket/123

# 同步主干
git fetch origin
git rebase origin/master

# 多个commit合并，进入交互模式
git rebase -i origin/master

# 推送到远程仓库，因为rebase以后，分支历史改变了，跟远程分支不一定兼容，有可能要强行推送
git push --force origin myfeature
```

## 合并commit选项

- pick：正常选中
- reword：选中，并且修改提交信息；
- edit：选中，rebase时会暂停，允许你修改这个commit（参考这里）
- squash：选中，会将当前commit与上一个commit合并，会有多个commit信息
- fixup：与squash相同，但不会保存当前commit的提交信息，会舍去commit信息
- exec：执行其他shell命令

## github pages:必须使用master作为分支

- hexo：添加文章后现hexo g（生成） hexo d（部署）
- jekyll：直接push到master就好

![Git 命令清单](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015120901.png)

[atlassian](https://www.atlassian.com/git)

# Git 风格指南

这份风格指南受到 [_How to Get Your Change Into the Linux Kernel_](https://www.kernel.org/doc/Documentation/SubmittingPatches)，[git man pages](http://git-scm.com/doc) 和大量社区通用实践的启发。

# 目录

1. [分支](#branches)
2. [提交](#commits)

  1. [消息](#messages)

3. [合并](#merging)

4. [杂项](#misc)

## Branches

- 选择_简短_和_具有描述性_的名字来命名分支：

  ```shell
  # 好
  $ git checkout -b oauth-migration

  # 不好，过于模糊
  $ git checkout -b login_fix
  ```

- 来自外部的标识符也适合用作分支的名字，例如来自 Github 的 Issue 序号。

  ```shell
  # GitHub issue #15
  $ git checkout -b issue-15
  ```

- 用破折号分割单词。

- 当不同的人围绕同一个特性开发时，维护整个团队的特性分支与每个人的独立分支是比较方便的做法。使用如下的命名方式：

  ```shell
  $ git checkout -b feature-a/master # team-wide branch
  $ git checkout -b feature-a/maria # Maria's branch
  $ git checkout -b feature-a/nick # Nick's branch
  ```

  合并时，由每个人的独立分支向全队的功能分支合并，最后合并到主分支。见[合并](#merging) 。

- 合并之后，除非有特殊原因，从上游仓库中删除你的分支。使用如下命令查看已合并的分支：

  ```shell
  $ git branch --merged | grep -v "\*"
  ```

## Commits

- 每个提交应当只包含一个简单的逻辑改动，不要在一个提交里包含多个逻辑改动。比如，如果一个补丁修复了一个 Bug，又优化了一个特性的性能，就将其拆分。
- 不要将一个逻辑改动拆分提交。例如一个功能的实现及其对应的测试应当一并提交。
- 尽早、尽快提交。出问题时，短小、完整的提交更容易发现并修正。
- 提交应当依_逻辑_排序。例如，如果 X 提交依赖于 Y，那么 Y 提交应该在 X 前面。

### Messages

- 使用编辑器编写提交信息，而非命令行。

  ```shell
  # 好
  $ git commit

  # 不好
  $ git commit -m "Quick fix"
  ```

  使用命令行会鼓励试图用一行概括提交內容的风气，而这会令提交信息难以理解。

- 概要行（即第一行）应当简明扼要。它最好不超过 50 个字符，首字母大写，使用现在时祈使语气。不要以句号结尾, 因为它相当于_标题_。

  ```shell
  # 好
  Mark huge records as obsolete when clearing hinting faults

  # 不好
  fixed ActiveModel::Errors deprecation messages failing when AR was used outside of Rails.
  ```

- 在那之后空一行，然后填写详细描述。每行不超过 _72 字符_，解释_为什么_需要改动, _如何_解决了这个 issue 以及它有什么_副作用_。

  最好提供相关资源的链接，例如 bug tracker 的 issue 编号：

  ```shell
  Short (50 chars or fewer) summary of changes

  More detailed explanatory text, if necessary. Wrap it to
  72 characters. In some contexts, the first
  line is treated as the subject of an email and the rest of
  the text as the body.  The blank line separating the
  summary from the body is critical (unless you omit the body
  entirely); tools like rebase can get confused if you run
  the two together.

  Further paragraphs come after blank lines.

  - Bullet points are okay, too

  - Use a hyphen or an asterisk for the bullet,
    followed by a single space, with blank lines in
    between

  Source http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
  ```

  最后，编写提交信息时，设想一下你一年以后再看这段提交信息时，希望获取什么信息。

- 如果 _提交 A_ 依赖于另一个 _提交 B_ ，在前者的 commit message 中应当指明。援引对应提交的 Hash。

  同理，如果 _提交 A_ 解决了 _提交 B_ 引入的 bug，这应当也被在 _提交 A_ 提及。

- 如果将一个提交 squash 到另一个提交，分别使用 `--squash` 和 `--fixup` 来强调目的。

  ```shell
  $ git commit --squash f387cab2
  ```

  _（Rebase 时使用 `--autosquash` 参数，标记的提交就会自动 squash。）_

## Merging

- **不要篡改提交历史。**仓库的历史本身就很宝贵，重要的是它能够还原_实际发生了什么_。对任何参与项目的人来说，修改历史是万恶之源。
- 尽管如此，有些时候还是可以重写历史，例如：

  - 你一个人孤军奋战，而且你的代码不会被人看到。
  - 你希望整理分支（例如使用 squash），以便日后合并。 最重要的，_不要重写你的 master 分支历史_ 或者任何有特殊意义的分支（例如发布分支或 CI 分支）。

- 保持你的提交历史_干净_、_简单_。_在你 merge_ 你的分支之前：

  1. 确保它符合风格指南，如果不符合就执行相应操作，比如 squash 或重写提交信息。
  2. 将其 rebase 到目标分支：

    ```shell
    [my-branch] $ git fetch
    [my-branch] $ git rebase origin/master
    # then merge
    ```

    这样会在 master 后直接添加一个新版本，令提交历史更简洁。

  _（这个策略更适合较短生命周期的分支，否则还是最好经常合并而不是 rebase。）_

- 如果你的分支包含多个 commmit , 不要使用快进模式。

  ```shell
  # 好；注意添加合并信息
  $ git merge --no-ff my-branch

  # 不好
  $ git merge my-branch
  ```

## Misc.

- 有许多工作流，每一个都有好有坏。一个工作流是否符合你的情况，取决于你的团队，项目，和你的开发规律。

  也就是说，重要的是认真 _选择_ 合适的工作流并且坚持。

- _保持统一_， 这涉及到从工作流到你的提交信息，分支名还有标签。 在整个 Repository 中保持统一的命名风格有助于辨认工作进度。

- _push 前测试_， 不要提交未完成的工作。

- 使用 [annotated tags](http://git-scm.com/book/en/v2/Git-Basics-Tagging#Annotated-Tags) 标记发布版本或者其他重要的时间点。

  个人开发可以使用 [lightweight tags](http://git-scm.com/book/en/v2/Git-Basics-Tagging#Lightweight-Tags)，例如为以后参考做标记。

- 定期维护，保证你的仓库状态良好，包括本地还有远程的仓库。

  - [`git-gc(1)`](http://git-scm.com/docs/git-gc)
  - [`git-prune(1)`](http://git-scm.com/docs/git-prune)
  - [`git-fsck(1)`](http://git-scm.com/docs/git-fsck)

# License

![cc license](http://i.creativecommons.org/l/by-nc/3.0/88x31.png)

This work is licensed under a Creative Commons Attribution-NonCommercial 4.0 International license.

# Credits

Agis Anastasopoulos / [@agisanast](https://twitter.com/agisanast) / <http://agis.io>

# Translators

- Qi Chen / aseaday@gmail.com
- chadluo / i@yuki.rocks

## Github

- issue and comment支持直接paste图片
- code block指定语言会高亮 "`jsx
- 创建一个 pull request 去修复 issue #234。那你可在 PR 输入「fixes #234」，就可以自动合并 PR 并关闭这个 issue
- 想链接到一个特定的评论，但无法做到？我在这里告诉你，点击名字旁边的日期/时间
- 代码或评论片段链接生成
- issue 创建list，
- 有project trello，可以将note转化issue
- 写wiki：处理非结构化的页面集合
- GitHub Pages + JekyII 将以最漂亮的主题来呈现你的 README.md
- 直接修改仓库文件会创建分支

## 扩展

- Git User Manual：客户端含有的文档
- [tiimgreen/github-cheat-sheet](https://github.com/tiimgreen/github-cheat-sheet)

## 工具

### tig

text-mode interface for git