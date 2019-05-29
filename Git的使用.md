# 一、Git 的使用

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



## 3. 将本地仓库关联到GitHub远程仓库

- 创建本地仓库（其实就是个文件夹）：在 E:/Git 下新建文件夹 Notes
- 在该文件夹下使用命令：`git init` 初始化一个本地仓库（初始化成功以后本文件夹后面会出现一个蓝色的（master）标识这个文件夹文一个本地仓库）
- 在Notes文件夹下创建一个 Test.txt 文件
- 第一步：
  - 添加Test.txt文件到库跟踪区：`git add Test.txt`（git add . 表示将整个文件夹添加到库跟踪区）
  - 查看Test.txt是否被添加到库跟踪区：`git status`
- 第二步：
  - 将库跟踪区改变的代码提交到本地代码库中：`git commit -m"first commit"`，引号内是注释
- 第三步：
  - 使用ssh秘钥链接本地仓库和 GitHub 远程仓库：`git remote add origin  git@github.com:RiverLee0101/Notes.git`
  - 此时已经把本地仓库Notes和远程仓库Notes关联起来了
- 第四步：
  - 上传本地文件到GitHub远程仓库：如果远程仓库为空白且第一次上传 `git push -u origin master`，以后就不用 -u
  - 如果远程仓库不是空的，则必须把远程仓库同步到本地：`git pull --rebase origin master`，然后再使用推送命令：`git push origin master` 上传



## 4. 新建develop分支并合并到master

- 创建develop分支并切换到develop分支：`git checkout -b develop` 这一条命令相当于 `git branch develop，git checkout develop`
- 查看当前分支：`git branch`，星号的就是当前分支
- 现在我们对此文件进行修改，第4条就是现在加的
- 然后提交:
  - `git add Git的使用.md`
  - `git commit -m"在分支develop上编辑的"`
- 切回master分支：`git checkout master`
- 切回master分支以后，查看 Git的使用.md 文件，刚才添加的内容应该不见了，因为那是提交到develop分支上，而master分支的提交点并没有改变
- 把develop分支上的工作成果合并到master上：`git merge develop`（用于将指定分支合并到当前分支）
- 合并完成就可以删除develop分支了：`git branch -d develop`



## 5. 推送本地分支到远程分支并建立关联

- 远程已有remote_branch 分支并且已经关联到本地local_branch，且已经切换到local_branch分支：
  - `git push`
- 远程已有remote_branch 分支但未关联本地local_branch分支，且已经切换到local_branch分支：
  - `git push -u origin/remote_branch`
- 远程没有remote_branch 分支，本地已经切换到local_branch分支：
  - `git push origin local_branch:remote_branch`



## 6. fork的使用

- 现在有一种情形，有一个叫Joe的程序员写了一个游戏程序，而你可能要去改进它，Joe将自己的代码放在了GitHub上，下面是你要做的事情：

  ![img](https://images2015.cnblogs.com/blog/736876/201704/736876-20170415203200580-1160875629.png)

  1. **Fork 他的仓库：**这个操作会复制Joe的仓库到你的GitHub账户下
  2. **Clone 你的仓库：**将这个远程仓库clone到本地计算机
  3. **更新某些文件：**现在可以对本地计算机的此仓库进行修改
  4. **提交你的更改：**更改以后按照 add-->commit 更新到本地仓库
  5. **将更改push到远程仓库：**push更新至自己的远程仓库
  6. **给Joe发送一个pull request：**如果你认为Joe会接受你的修改，给他发送一个pull request，他接收以后，修改的内容就同步至他的仓库



# 二、Git 命令大全

## 1. 本地仓库与远程仓库同步

- 初始化Git仓库：`git init`
- 添加到库跟踪区：`git add .`
- 提交到代码库中：`git commit -m"some instructions"`
- 查看分支的状态：`git status`
- 关联本地和远程：`git remote add origin  git@github.com:RiverLee0101/Notes.git`
- 同步本地和远程：`git push -u origin master`（远程为空且第一次上传）
- 同步本地和远程：`git push origin master`（非第一次上传）
- 同步远程和本地：`git pull --rebase origin master`
- 同步远程和本地：`git pull origin master`(将远程origin的master分支拉取过来和本地的当前分支合并)



## 2. 分支的相关使用

- 创建新分支：`git branch new_branch`
- 切换到分支：`git checkout new_branch`
- 创建并切换：`git checkout -b new_branch`
- 查看本地分支：`git branch`
- 查看远程分支：`git branch -r`
- 查看所有分支：`git branch -a`
- 删除某个分支：`git branch -d new_branch`
- 合并某个分支：`git merge new_branch`（在master分支下）
- 本地远程关联：`git checkout -b new_branch origin/develop`（新建一个本地分支new_branch并与远程develop分支关联）



## 3. clone远程仓库

- clone远程master分支：`git clone git@gitlab.vmic.xyz:exapp-search/oversea-appsearch.git`
- clone远程develop分支：`git clone -b develop git@gitlab.vmic.xyz:exapp-search/oversea-appsearch.git`



# 四、问题解疑

## 1. commit、pull、push过程

- 为什么要先commit，然后pull，然后再push，我pull了，岂不是把自己改的代码都给覆盖掉了嘛，因为远程没有我改的代码，我pull，岂不是覆盖了我本地的改动好的地方了？那我还怎么push？

  > 这个先 commit 再 pull 再 push 的情况就是为了应对多人合并开发的情况：
  > 1、commit 是为了告诉 git 我这次提交改了哪些东西，不然你只是改了但是 git 不知道你改了，也就无从判断比较；
  > 2、pull是为了本地 commit 和远程commit 的对比记录，git 是按照文件的行数操作进行对比的,如果同时操作了某文件的同一行那么就会产生冲突，git 也会把这个冲突给标记出来，这个时候就需要先把和你冲突的那个人拉过来问问保留谁的代码，然后在 git add && git commit && git pull 这三连，再次 pull 一次是为了防止再你们协商的时候另一个人给又提交了一版东西,如果真发生了那流程重复一遍，通常没有冲突的时候就直接给你合并了，不会把你的代码给覆盖掉；
  >
  > 3、出现代码覆盖或者丢失的情况：比如A B两人的代码pull 时候的版本都是1，A在本地提交了2，3并且推送到远程了，B 进行修改的时候没有commit 操作，他先自己写了东西，然后 git pull 这个时候 B 本地版本已经到3了，B 在本地版本3的时候改了 A 写过的代码，再进行了git commit && git push 那么在远程版本中就是4，而且 A 的代码被覆盖了，所以说所有人都要先 commit 再 pull,不然真的会覆盖代码的。