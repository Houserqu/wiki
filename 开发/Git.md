# Git

 ## 概念

![git](http://qiniu.houserqu.com/ec7210655b4d4fc4afcd1466d9aa2343~tplv-k3u1fbpfcp-zoom-1.image)

[git合并原理](https://zhuanlan.zhihu.com/p/149287658)

全局配置文件：`~/.gitconfig`

## 操作

### SSH 授权

1. 根据邮箱生成公私钥 `ssh-keygen -t rsa -C "你账号邮箱地址"`

2. `~/.ssh` 目录下，复制 `id_rsa.pub` 的公钥内容，保存到 Git 平台上（如 github，gitlab）

3. 全局配置 Git 的该邮箱和用户名

   ```
   git config --global user.name "xxx"
   git config --global user.email "xxx@xx.com"
   ```

### 添加远程仓库地址

```bash
git remote add origin <git url>
```

### checkout

```bash
git checkout <branch>        # 切换分支
git checkout -b <new branch> # 创建新分支并切换到该分支
git checkout <commit id>     # 检出到指定提交记录
```

### fetch

拉取远程分支，但是不进行本地合并操作

```bash
git fetch <远程主机名> <分支名> # 获取远程仓库特定分支的更新
git fetch --all              # 获取远程仓库所有分支的更新
```

### pull

```bash
# 从远程仓库拉取代码并合并到本地，可简写为 git pull 等同于 git fetch && git merge 
git pull <远程主机名> <远程分支名>:<本地分支名>
# 使用rebase的模式进行合并
git pull --rebase <远程主机名> <远程分支名>:<本地分支名>
```

### branch

```bash
git branch <branch-name>  # 新建本地分支，但不切换
git branch # 查看本地分支
git branch -r # 查看远程分支
git branch -a # 查看本地和远程分支
git branch -D <branch-nane> # 删除本地分支
git branch -m <old-branch-name> <new-branch-name> # 重新命名分支
```

### rebase / merge

都是进行合并操作，rebase 会变基，适合仅个人开发的分支，能够让提交更清晰，merge 适合多人开发的分支。

```bash
git rebase -i ac18084 # 将 ac18084 之后的提交压缩成一个 commit
```

### cherry-pick

获取某个分支的若干 commit 合并到当前分支

```bash
git cherry-pick <first-commit-id>...[<last-commit-id>] # 一个或范围 commit
# 出现冲突，解决完之后
git add
git cherry-pick --continue
```

### log

```bash
git log                    # 显示提交的用户、日期、comment
git log --stat             # 显示提交修改的文件和代码量
git log --oneline          # 一行显示提交信息
git log --graph --oneline  # 分支图的形式显示并一行显示提交信息
git log -p filenam         # 查看文件提交历史
```

### reflog

查看操作记录，可用于恢复误操作

```bash
git reflog
```

### alias

配置操作别名（zsh 默认会提供系统级别的 alias），推荐用 g 代替 git  `alias g=git`。

```bash
git config --global alias.<简化的字符> 原始命令
# 示例
git config --global alias.co checkout
```

通过文件配置 `~/.gitconfig`

```
[alias]
st = status -sb
mt = mergetool
last = log -1 HEAD
lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
```

### tag

```bash
# 删除远程tag （先 pull 使本地有这个 tag，然后本地删除，push 到远程）
git tag -d tag_name
git push origin :refs/tags/tag_name
```

### revert/reset

revert 用一个新的提交撤回之前的某个提交，适合撤销一些 commit 中若干 commit，且不影响其他 commit

reset 退回到指定的 commit 上

```sql
--soft  – 缓存区和工作目录都不会被改变
--mixed – 默认选项。缓存区和你指定的提交同步，但工作目录不受影响
--hard  – 缓存区和工作目录都同步到你指定的提交

git reset --soft <commit id / HEAD^ / HEAD~1>

// 放弃本地更改，强制更新到远程分支状态（适用于更新被 rebase 过的分支）
git reset --hard origin/master
```

### 修改 commit message

```bash
# 最近一次 commit 的 message (不要修改已经 push 的公共分支，因为 amend 后 id 会变)
git commit --amend              # 交互模式
git commit --amend -m 'message' # 直接修改

# 修改历史 commit（719466） 的 mesage
git rebase -i <commit id>  # 使用 rebase 到 719466 的上一个 commit 处，在弹出文件中修改 719466 的 commit 为 edit，此时 rebase 到这里到时候会停下 
git commit --amend    # 然后修改上一个 commit（719466）
git rebase --continue # 继续 rebase 回到最新的 commit
```

### stash

```bash
git stash                # 把本地的改动暂存起来
git stash save "message" # 执行存储时，添加备注，方便查找。
git stash pop            # 应用最近一次暂存的修改，并删除暂存的记录
git stash apply          # 应用某个存储,但不会把存储从存储列表中删除，默认使用第一个存储, 添加 stash@{$num} 参数指定记录
git stash list           # 查看所有 stash
git stash clear          # 删除所有缓存的 stash
```

**恢复删除的stash**

```bash
# 1.找出所有的 stash 提交记录
git fsck --unreachable | grep commit | cut -d ' ' -f3 | xargs git log --merges --no-walk
# 2.恢复指定 stash
git update-ref refs/stash 4b3fc45c94caadcc87d783064624585c194f4be8 -m "My recovered stash"
```

### .gitignore

```bash
# .gitignore只能忽略那些原来没有被 track 的文件，如果某些文件已经被纳入了版本管理中，则修改 .gitignore 是无效的。解决方法是先把本地缓存删除，然后再提交。
git rm -r --cached .  # 删除所有文件的缓存
git rm --cached logs/xx.log # 删除指定文件的缓存
```

### clean

```bash
# 删除 untracked 文件
git clean -n -d # 查看将会删除的文件
git clean -f    # 执行删除
```