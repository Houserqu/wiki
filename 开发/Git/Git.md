# Git

[常用命令思维导图](Git%20b8a5ff29aece46eab3a16c3d67073ab0/%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE%206f21336703f34165ba855ef8a2270f50.md)

### 添加远程仓库地址

```bash
git remote add origin <git url>
```

## checkout

```jsx
git checkout <branch>        # 切换分支
git checkout -b <new branch> # 创建新分支并切换到该分支
git checkout <commit id>     # 检出到指定提交记录
```

## log

```jsx
git log                    # 显示提交的用户、日期、comment
git log --stat             # 显示提交修改的文件和代码量
git log --oneline          # 一行显示提交信息
git log --graph --oneline  # 分支图的形式显示并一行显示提交信息
```

## reflog

查看操作记录，可用于恢复误操作

```bash
git reflog
```

### Tag

```bash
# 删除远程tag （先 pull 使本地有这个 tag，然后本地删除，push 到远程）
git tag -d tag_name
git push origin :refs/tags/tag_name
```

### reset

撤销提交

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

### 恢复stash

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