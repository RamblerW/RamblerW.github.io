- 查看文件修改历史

```
git blame file_name
git show commitID
```

- 将某个分支的某次提交合并到另外一个分支：`git cherry-pick 版本号（如 git cherry-pick b65b62a）`

- 查看远程仓库：`git remote -v`

- 查看远程分支：`git branch -a`

- 查看本地分支：`git branch`

- 删除本地分支：`git branch -d branchName`

- 切换远程仓库：`git remote set-url origin newUrl`

- 更新本地的远程分支信息：`git fetch origin`

- 拉取远程分支到本地：`git checkout -b branchName origin/branchName`

- 提交代码
  - 将修改添加至本地缓存：`git add .`
  - 将本地缓存保存到本地仓库：`git commit -m 'msg'`
  - （初次提交）连接到远程仓库：`git remote add origin 仓库地址 `
  - 将本地仓库推送到远程：`git push` 或 `git push -u origin master`

- 修改git上传文件大小限制为500M：`git config --global http.postBuffer  524288000`

