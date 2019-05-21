# Git的使用

## 1. 安装git和生成ssh秘钥

- 下载安装：<https://gitforwindows.org/>

- 打开Git Bash

- 在Git Bash中使用：`ssh-keygen -t rsa -C "公司邮箱地址"`，生成对应的gitlab秘钥：*id_rsa*和*id_rsa.pub*

- 进入：C:\Users\11101453\ .ssh，将id_rsa.pub中的内容复制到公司的gitlab公钥上

- 在gitbash中使用`ssh-keygen -t rsa -C "github地址" -f ~/.ssh/github_rsa`生成对应的github密钥： *github_rsa* 和 *github_rsa.pub*

- 将 github 公钥即 *github_rsa.pub* 中的内容配置到自己的 github 上

- 进入秘钥生成的位置：`cd ~/.ssh`

- 新建一个 config 文件：`touch config`，并添加如下配置：

  ```config
  # gitlab
  Host gitlab
      HostName gitlab.vmic.xyz #这里填你的gitlab的Host
      User git
      IdentityFile ~/.ssh/id_rsa
  # githab
  Host github.com
      HostName github.com
      User git
      IdentityFile ~/.ssh/github_rsa
  ```



## 2. 测试连接

- 在Git Bash中分别输入：

  - `ssh -T git@gitlab`
  - `ssh -T git@github.com`

  ```
  catalinaLi@catalinaLi MINGW64 ~/.ssh
  $ ssh -T git@gitlab
  Welcome to GitLab, @11101453!
  
  catalinaLi@catalinaLi MINGW64 ~/.ssh
  $ ssh -T git@github.com
  Hi RiverLee0101! You've successfully authenticated, but GitHub does not provide shell access.
  ```

- 到这一步，本电脑就可以和Git远程仓库进行连接了



## 3. 将本地项目同步到GitHub远程仓库

- 创建本地仓库（其实就是个文件夹）：在 E:/Git 下新建文件夹 Notes
- 在该文件夹下使用命令：`git init` 初始化一个本地仓库（初始化成功以后本文件夹后面会出现一个蓝色的（master）标识这个文件夹文一个本地仓库）
- 在Notes文件夹下创建一个 Test.txt 文件
- 第一步：
  - 添加Test.txt文件到库跟踪区：`git add Test.txt`（git add . 表示将整个文件夹添加到本地仓库）
  - 查看Test.txt是否被添加到库跟踪区：`git status`
- 第二步：
  - 将库跟踪区改变的代码提交到本地代码库中：`git commit -m"first commit"`，引号内是注释
- 第三步：
  - 使用ssh秘钥链接本地仓库和 GitHub 远程仓库：`git remote add origin  git@github.com:RiverLee0101/Notes.git`
  - 此时已经把本地仓库Notes和远程仓库Notes关联起来了
- 第四步：
  - 上传本地文件到GitHub远程仓库：如果远程仓库为空白且第一次上传 `git push -u origin master`，以后就不用 -u
  - 如果远程仓库不是空的，则必须把远程仓库同步到本地：`git pull --rebase origin master`，然后再使用推送命令：`git push origin master` 上传