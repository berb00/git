# git note

## 初始化、上传git仓库流程

  1.GitHub上新建仓库 或 查看已连接的远程库//git remote -v
  2.git remote add origin git@github.com:michaelliao/learngit.git             // ssh支持的原生git协议速度最快。
    git remote add origin https://github.com/berb00/git.git                   // 连接到远程仓库      https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令
  3.git pull origin [branchname]              // 拉取远程库分支信息
  4.git push -u origin branchname             // 第一次把本地库的所有内容推送到远程库上 (远程库的名字就是origin，这是Git默认的叫法)
                                              // -u:第一次推送分支时把本地分支内容推送的远程分支并把本地分支和远程分支关联起来，在以后的推送或者拉取时就可以简化命令。
  5.git push origin branchname                // 之后的提交
  6.git clone https://github.com/berb00/branchname.git     //克隆远程仓库到本地

## git branch

    1.master    主分支 用来发布版本
    2.develop   branch from master/push to release 
    3.releases  branch from develop/push to develpo and master at the same time
    4.features  branch from develop/push to develop 团队成员直接操作的具体功能开发分支
    5.fixs      branch from develop/push to develop (bugfix for develop  it`s a temporary branch)
    6.hotfixs   branch from master/push to master   (bugfix for master   it`s a temporary branch)

## tips

    查看终端打印方式
        向下翻页:Space
        向上翻页:b
        退出:q

    git是分布式的 以元数据存储而非文件 其跟踪并管理的是修改而非文件

    .git是版本库目录

    stage（或者叫index）暂存区

    Git自动创建的第一个分支master，以及指向master的一个指针叫HEAD

## git options

    -d      --delete
    -D      --delete --force
    -f      --force
    -m      --move 移动或重命名
    -m      --move --force
    -r      --remote
    -a      --all

## configure ssh

    1.create secret key
        ssh-keygen -t rsa -C 'email'
    2.copy the public key to github`settings-SSH keys
    3.copy the secret key file to .ssh directory
    4.chmod 600 id_rsa // 防止没有权限或权限过大
    5.test the connections to github  
        ssh -T git@github.com
    6.set the remote origin
        git remote set-url aliasname SSHurl

## git error

    1、Git: fatal: The remote end hung up unexpectedly
        git config --global http.postBuffer 1048576000
        git config --global http.postBuffer 1048576000
    2、Git error: RPC failed; curl 56 LibreSSL SSL_read: SSL_ERROR_SYSCALL, errno 54
        使用 ssh 方式

## add new remote branch
    git branch <branchname>
    git swicth <branchname>
    git push --set-upstream origin <branchname>

## trailing whitespace
    代码中不允许以空格结尾


    已修改    ---add--->     已暂存     ---commit--->     已提交
    modified                staged                       committe



    Untracked files: 未跟踪状态(新建未经过add的文件)
    Changes to be committed: 已暂存状态

    Changes not staged for commit:已跟踪文件的内容发生了变化，但还没有放到暂存区(使用add进行暂存)
    Changes to be committed:

## 记住git提交密码
    git config --global credential.helper store

    