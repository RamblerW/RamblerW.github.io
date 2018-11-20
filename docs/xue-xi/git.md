# Git 学习笔记

1. 查看文件修改历史
   ```
   git blame file_name
   git show commitID
   ```
2. 提交更改异常，错误信息中出现_**git config –global user.name "username"**_字样

   * 解决方案：在终端依次执行以下命令（请更改为自己的邮箱和用户名）：
     ```
     git config --global user.email "rambler@feiyi.com.cn"
     git config –global user.name "rambler"
     ```

3. 将某个分支的某次提交合并到另外一个分支

   ```
   git cherry-pick 版本号（如 git cherry-pick b65b62a）
   ```



