#Git
# Reference

- [Git Command Exploer](https://gitexplorer.com/)
- [Pro Git](https://git-scm.com/book/en/v2)
- [Git 教程 - 廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)
- [常用 Git 命令清单 - 阮一峰](https://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
- [Git 原理入门](https://www.ruanyifeng.com/blog/2018/10/git-internals.html)

# 克隆远程指定分支到本地

```bash
# 克隆远程 dev 分支到本地
git clone <url> -b dev

# 克隆远程 master / main 分支到本地 (默认分支)
git clone <url>
```

# 查看远程分支

```bash
git remote -v
```

# 同步远程分支列表

```bash
git fetch -p

git remote update origin --prune
```

# 删除远程分支

```bash
# 删除远程 remoteBranchName 分支
git push origin --delete remoteBranchName
```

# 查看本地分支

```bash
git branch

# 查看本地所有分支
git branch -a
```

# 查看本地分支状态

```bash
git status
```

# 删除本地分支

```bash
# 删除本地 local 分支
git branch -delete local # git branch -d local

# 强制删除本地 local 分支
git branch -D local
```

# 本地创建新分支

```bash
# 创建 new_branch 分支并切至该分支
git checkout -b new_branch

# 仅创建 another_new_branch 分支但不切至该分支
git branch another_new_branch
```

# 切换本地分支

```bash
# 切换至本地 another 分支 (检出)
git checkout another
```

#  本地分支推送到远程指定分支

```bash
# 本地 local 分支推送到远程 origin 分支
git push origin local:origin

git push -u origin remoteBranchName
```

# 拉取远程指定分支并合并到本地分支

```bash
# 拉取远程 dev 分支并合并到本地分支
git pull origin dev
```

# 本地创建新分支并拉取远程分支

本地创建新分支 `local_sample`, 并与远程分支 `origin_sample` 同步, 同时本地切换到 `local_sample` 分支:

```bash
git checkout -b local_sample origin/origin_sample
```

# 本地分支合并至远程分支

```bash
# 切换至本地 local 分支
git checkout local
# 拉取远程 local 分支最新代码
git pull origin local

# 切换至本地 dev 分支
git checkout dev
# 拉取远程 dev 分支最新代码
git pull origin dev
# 将本地 local 分支代码合并至本地 dev 分支
git merge local
# 将本地 dev 分支代码推送至远程 dev 分支
git push origin dev
```

# 查看所有跟踪文件

```bash
git ls-files
```

# 删除文件

```bash
git rm <filename>
git rm <filename> -f
```

# 移动文件

```bash
git mv <oldfile> <newfile>
```

# 查看提交信息

- [2.3 Git Basics - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

```bash
git log
```

# 克隆远程指定文件夹到本地

```bash
mkdir local_project_name
cd local_project_name
git init

git remote add -f origin <remote-repo-url>
git config core.sparsecheckout true  # 开启 sparse clone

echo <specified-folder> >> .git/info/sparse-checkout # 设定指定文件夹
git pull origin <remote-branch> # 拉取远程仓库分支
```

示例；

```bash
mkdir thrid_login_flutter
cd thrid_login_flutter
git init
git remote add -f origin https://github.com/zeqinjie/thrid_login_demo.git
git config core.sparsecheckout true
echo "thrid_login_flutter" >> .git/info/sparse-checkout
git pull origin main
```

上述示例中原仓库 `thrid` 为笔误, 实际应为 `third`

# fatal: refusing to merge unrelated histories

- [The “fatal: refusing to merge unrelated histories” Git error](https://www.educative.io/answers/the-fatal-refusing-to-merge-unrelated-histories-git-error)

```bash
git pull origin master --allow-unrelated-histories
```

# 删除误上传到远程仓库的文件或者文件夹

- [Git 如何忽略已经上传的文件或文件夹？](https://blog.csdn.net/weixin_43352244/article/details/120842927)

```bash
git rm -r --cached <file name or folder name>
```

执行上述命令后, 重新提交代码即可删除掉远程相应的文件或文件夹。

# 撤回本地提交

撤回本地上一次提交, 但保留代码和新添加文件:

```bash
git reset --soft HEAD^
git reset --soft HEAD~1
```

撤回本地两次提交:

```bash
git reset --soft HEAD~2
```

`--soft` 表示**软**撤回, 不删除本地代码和新添加文件, 只撤回提交信息;

`--hard` 表示**硬**撤回, 删除本地代码和新添加文件, 并撤回提交信息。

```bash
git reset --merge HEAD~1
```

# 远程仓库回滚

回滚上一次提交:

```bash
git revert HEAD

git status

git push origin dev
```

`git revert HEAD` 后需要填写提交信息, 随后提交上去即可在远程仓库上看到形如 `Revert "..."` 的提交信息。

# 回滚本地代码

根据 `commit id` 回滚:

```bash
git reset --hard <commit id>
```

在回滚前须查看 `commit id`:

```bash
git log
```

使用向下方向键查看更多 `commit` 信息。

# 提交多行信息

```bash
git commit 'This is first line,
this is second line'
```

# 检索 git 日志

通过作者检索:

```bash
git log --author <author name>
```

通过提交关键字检索:

```bash
git log --grep <keywords>
```

通过文件名检索:

```bash
git log -p -- README.md

git log -p -- public/fonts/font.ttf
```
