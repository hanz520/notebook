# git 命令

## 基本操作

```bash
git init    // 初始化git版本库

git add [file]    // 添加文件到暂存区

git add .   // 他会监控工作区的状态树，使用它会把工作时的所有变化提交到暂存区，包括文件内容修改(modified)以及新文件(new)，但不包括被删除的文件。

git add -u  // 他仅监控已经被add的文件（即tracked file），他会将被修改的文件提交到暂存区。add -u 不会提交新文件（untracked file）。（git add --update的缩写）

git add -A  // 是上面两个功能的合集（git add --all的缩写）

git commit -m [说明文字]        // 提交到git仓库

git commit -am "some str"     // 添加到暂存区并且提交到仓库

git commit --amend    // 追加提交，不新增commit-id

git status    // 查看仓库当前状态

git diff  // 查看当前未提交的内容和仓库中的差异，可以查看单个文件的差异

git log // 查看提交的历史记录  

// HEAD代表当前版本，HEAD^代表上一版本，HEAD^代表往前第二个版本，HEAD~100往前第一百个版本

git log --pretty=oneline   // 美化版的查看提交的历史记录

git reset --hard HEAD^    // 版本回退，回退到上一个版本

git reflog  // 查看git仓库的每一次命令

git checkout -- file   // 丢弃工作区，放弃对文件的修改

git reset HEAD <file>   // 把暂存区的修改撤销掉（unstage）

git rm <file>   // 删除文件

git rebase --abort    // 终止rebase
```

## 远程仓库相关

```bash
git remote add origin git@server-name:path/repo-name.git    // 本地库关联一个远程库

git clone git@github.com:michaelliao/gitskills.git    // 复制一个远程仓库

git push -u origin master   // 第一次推送master分支的所有内容

git push origin master    // 推送最新修改

git pull    // 拉取远程代码

git pull --allow-unrelated-histories    // 允许合并不相关历史的内容

git pull --rebase    // 拉取远程代码，避免出现"Merge branch 'master' of ..." 这类垃圾日志

git push    // 推送代码

git remote    // 查看远程库信息
git remote -v

git checkout -b dev origin/dev    // 创建远程origin的dev分支到本地

git branch --set-upstream-to=origin/dev dev   // 指定本地dev分支与远程origin/dev分支的链接

git rebase    // 变基   将git提交历史变成一条直线

git push origin dev:dev   // 推送dev分支到远程仓库

git push origin :dev    // 删除远程dev分支
git push origin --delete dev    // 删除远程dev分支

git checkout -b 本地分支名 origin/远程分支名    // 创一个和远程分支一样的分支 -- 拉取分支
/** 如果报错：'origin/dev' is not a commit and a branch 'dev' cannot be created from it
  * 在创建远程分支到本地之前 git pull 就好
*/
git push origin 分支名 --force   // 强制提交当前版本号，以达到撤销版本号的目的(撤销推送到远程的commit)

git branch -r 查看远程分支
```

## 版本管理

```bash
git checkout -b dev   // git checkout命令加上-b参数表示创建并切换，这里切换到了dev，等同于下面两条命令

git branch dev    // 创建分支dev

git checkout dev  // 切换到分支dev

git branch  // 查看当前分支

git merge dev   // 合并dev分支到当前分支

git branch -d dev   // 删除dev分支

git log --graph   // 查看分支合并图

git log --graph --pretty=oneline --abbrev-commi   // 查看分支合并情况 美化版

// 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

// git merge --no-ff -m "merge with no-ff" dev    // 表示禁用Fast forward的合并。合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并

git branch -D <name>    // 强行删除没有合并过的分支
```

## 储藏功能
```bash
git stash   // 把当前手头的工作储藏起来，进行其他优先级更高的工作

git stash list  // 查看储藏的工作现场

git stash apply   // 恢复工作现场。 恢复后，stash内容并不删除，你需要用git stash drop来删除

git stash apply stash@{0}

git stash pop   // 恢复工作现场，同时把stash内容也删了

```

## 标签管理
```bash
git tag <name>    // 打一个新标签

git tag   // 查看标签列表

git tag <name> f52c633    // 对指定版本打标签

git show <tagname>    // 查看标签信息

git tag -d <tagname>    // 删除标签

git push origin <tagname>   // 推送某个标签到远程

git push origin --tags    // 推送所有本地标签到远程仓库

git push origin :refs/tags/v0.9   // 本地某个标签已经删除，该命令删除远程仓库的改标签



```
**标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签**

## 撤回已经推送到远程的代码

1. 先通过`git reset –soft <版本号>`或者`git reset –hard <版本号>`将本地的分支返回到指定commit
2. 再通过`git push origin <分支名> –force`推送到远程