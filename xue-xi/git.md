- 查看文件修改历史

```git
git blame file_name
git show commitID
```

- 查看远程仓库：`git remote -v` 
- 查看远程分支：`git branch -a`
- 查看本地分支：`git branch`
- 删除本地分支：`git branch -d branchName`
- 切换远程仓库：`git remote set-url origin newUrl`
- 更新本地的远程分支信息：`git fetch origin`
- 拉取远程分支到本地：`git checkout -b branchName origin/branchName`
- 查看本地更改：`git status`
- 放弃本地更改：`git reset --hard`
- 提交代码
  - 将修改添加至本地缓存：`git add .`
  - 将本地缓存保存到本地仓库：`git commit -m 'msg'`
  - （初次提交）连接到远程仓库：`git remote add origin 仓库地址 `
  - 将本地仓库推送到远程：`git push` 或 `git push -u origin master`
- 修改 git 文件大小限制为500M：`git config --global http.postBuffer 524288000`
- 设置最低速度时间：`git config --global http.lowSpeedLimit 0`、`git config --global http.lowSpeedTime 999999`
- 将某次提交（086da18）的代码合并到另一分支：`git cherry-pick 086da18`
- 设置用户名：`git config --global user.name "nameVal"`
- 设置密码：`git config --global user.email "email@qq.com"`



---

报错：fatal: The remote end hung up unexpectedlyfatal: early EOFfatal: index-pack failed

解决：https://stackoverflow.com/questions/21277806/fatal-early-eof-fatal-index-pack-failed

```
git config --global core.compression 0
git clone --depth 1 <repo_URI>
// 检出后进入目录
git fetch --unshallow
git pull --all
```

