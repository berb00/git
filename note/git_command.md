# git command

## Main Porcelain Commands
### init
    git init                            // 创建版本库 (生成例：/.git/目录)


### clone
    git clone <adderss>                 // 克隆一个已有的远程仓库。address是远程库地址
    

### add
    git add <file>                      // 用于把文件添加到git（暂存区），准备提交
    git add -A  或者 git add -all       // 把工作区的所有修改添加到暂存区
    git add .                           // 提交所有文件到暂存区
    git add -i  (--interactive)         // 交互式终端模式


### commit
    git commit -m 'comment'             //把暂存区的所有内容提交到当前分支 只有添加文件之后才能使用，用于提交内容到主分支（默认是master）


### pull      
    git push -u origin branchname             // 第一次把本地库的所有内容推送到远程库上 (远程库的名字就是origin，这是Git默认的叫法)
    git push origin branchname                // 之后的提交
    git pull remotealias // 不确定是否拉取所有分支
    git pull remotealias remotebranch // 拉取远程分支并与本地分支合并(默认当前分支)
    git pull remotealias remotebranch:localbranch   //  相当于：
        1.git fetch remotealias remotebranch
        2.git merge localbranch


### push


### fetch
    git fetch remotealias   // 拉取远程仓库到本地仓库 (默认master分支)
    git fetch remotealias branchname   // 拉取远程指定分支到本地仓库 (成功后返回一个FETCH_HEAD) // git log -p FETCH_HEAD


### rm
    git rm --cached <file>              // 从暂存区撤回commit内容:(会删除文件已commit文件)
    git rm <file>                       // 删除文件。删除之后还需要提交（git commit）


### merge
    #merge
        git merge branchname                // 合并branchname分支到当前分支
        git merge --no-ff <branch>          // 关闭Fast-forward 合并（快速模式），强制禁用快速合并模式进行合并指定分支到当前分支
        git merge --no-ff branchname        // 合并分支
        #合并分支
            1.在master分支操作一个文件1.txt(例如加入一段信息)    add commit      master分支上的操作
            2.创建并切换至另一分支a,操作该文件(再加入一段信息)    add commit      a分支上的操作
            3.切换至master分支 查看1.txt(无法显示a分支下的操作)
            3.git merge a//把a分支的工作成果合并到master分支上   Fast-forward:“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。
            4.查看1.txt(可显示a分支下的操作)

### branch

    git branch                                            // 查看本地分支
    git branch -r                                         // 查看远程分支
    git branch -a                                         // 查看所有分支
    git branch branchname                                 // 新建分支
    git branch -d branchname                              // 删除分支
    git branch -D branchname                              // 强制删除  
    git branch -d -r branchname                           // 删除远程分支并推送
    git push origin:branchname                            // 删除分支后推送
    git branch -m oldbranchname newbranchname             // 重命名本地分支

    git branch [<选项>] [-r | -a] [--merged | --no-merged]
    git branch [<选项>] [-l] [-f] <分支名> [<起始点>]
    git branch [<选项>] [-r] (-d | -D) <分支名>...
    git branch [<选项>] (-m | -M) [<旧分支>] <新分支>
    git branch [<选项>] (-c | -C) [<老分支>] <新分支>
    git branch [<选项>] [-r | -a] [--points-at]
    git branch [<选项>] [-r | -a] [--format]

### checkout

    git checkout <branch>                                 // 切换到指定分支
    git checkout -b <newbranch>                           // 创建一个新的分支并切换到这个新的分支。-b参数表示创建新分支 newbranch 新的分支名
    git checkout branchname                               // 切换到某分支
    git checkout -- <file>                                // 丢弃工作区的修改
    git checkout -- <file>                                // 放弃在工作区的更改     //就是让这个文件回到最近一次git commit或git add时的状态 撤销文件的修改到最近一次git commit或者git add 注意：--非常重要 
        add前形成的修改(未再add):                             // 撤销修改就回到和版本库一模一样的状态
        add后形成的修改(未再add):                             // 撤销修改就回到添加到暂存区后的状态。

### log

    git log                                               // 由近及远返回commit历史记录(提交日志)
    git log --pretty=online(单行显示---长hash)             // 查看版本历史记录-简化输出日志
    git log --online(单行显示---短hash)                    // 查看版本历史记录  
    git log --graph                                       // 显示分支合并图
    git log -p -2			                                    // -p:显示每次提交的内容差异。-2:仅显示最近两次提交：


### shortlog


### show
git log [<选项>] [<版本范围>] [[--] <路径>...]
git show [<选项>] <对象>...
    -q, --quiet           不显示差异输出
    --source              显示源
    --use-mailmap         使用邮件映射文件
    --decorate-refs <模式> 只修饰与 <模式> 匹配的引用
    --decorate-refs-exclude <模式> 不修饰和 <模式> 匹配的引用
    --decorate[=...]      修饰选项
    -L <n,m:file>         处理文件中第 n 到 m 之间的行，从 1 开始

### status

    git status			检查当前文件状态
    git status -s
    git status --short 	状态简览

### reset

    git reset HEAD <file>               // 把暂存区的修改回退到工作区（把暂存区的修改撤销掉清除 （unstage），重新放回工作区）
    git reset --hard HEAD^              // 把当前版本回退到上一个版本
    git reset --hard commitId           // HEAD指针指向commitId版本    
    git reset --hard <commit_id>        //把工作区内容恢复到指定版本
    前进回退版本号:
        1.使用索引值
        git reset --hard 局部索引值
        2.使用^符号(只能后退)
        git reset --hard HEAD^ // 回退一步
        git reset --hard HEAD^^ // 回退二步
        git reset --hard HEAD^ // 回退三步
        3.使用~符号(只能后退)
        git reset --hard HEAD~n // 回退n步
        --soft    //在本地库移动HEAD指针
        --mixed   //在本地库移动HEAD指针/重置暂存区
        --hard    //在本地库移动HEAD指针/重置暂存区/重置工作区

### stash

    git stash                           //保存当前分支工作现场，可以执行多次
    git stash save 'msg'                //保存当前分支工作现场，并添加备注
    git stash list                      //查看当前分支保存的工作现场列表
    git stash show
    git stash apply [stash_id]          //恢复现场，方括号内是可选参数（指定恢复）
    git stash pop [stash_id]            //恢复现场，并删除
    git stash drop [stash_id]           //删除现场
    git stash clear                     //删除所有缓存stash

### tag    
    git tag -l                                  // 查看已打的标签
    git tag -l "v1.8.5*"                        // 查看某个系列的标签
    git tag <tagname>                           // 打一个轻量标签
    git tag -a <tagname> -m "my version 1.4"    // 打一个附注标签
    git tag -d <tagname>                        // 删除标签
    git push origin --delete <tagname>          // 删除远程标签
    git tag -a v1.2 9fceb02                     // 后期打标签
    git push origin <tagname>                   // 推送标签到共享服务器上
    git push origin --tags                      // 把所有不在远程仓库服务器上的标签全部传送到那里
    git checkout 2.0.0                          // 检出标签(注:会使仓库处于“分离头指针（detacthed HEAD）”的状态-有副作用)

    
### am


### archive


### bisect


### bundle


### cherry-pick


### citool


### clean
    git clean --dry-run         // 预览将要删除的未被追踪的文件
    git clean -n                // 预览将要删除的未被追踪的文件
    git clean -f                // 删除未被追踪的文件(.gitignore指定的文件除外)
    git clean -f <path>         // 删除指定路径下的没有被track过的文件
    git clean -df               // 删除当前目录下没有被track过的文件和文件夹
    git clean -xf               // 删除当前目录下所有没有track过的文件. 不管他是否是.gitignore文件里面指定的文件夹和文件


### describe


### diff    
    git diff                            //查看修改的内容。注意：已经使用git add之后，不能再查看修改的内容


### format-patch


### gc


### gitk


### grep


### gui


### mv
    git mv <filedir> <newfiledir>       //移动文件到新的路径，如果新的文件名发生改变，则可以理解为重命名


### notes

git notes [--ref <注解引用>] [list [<对象>]]
git notes [--ref <注解引用>] add [-f] [--allow-empty] [-m <说明> | -F <文件> | (-c | -C) <对象>] [<对象>]
git notes [--ref <注解引用>] copy [-f] <源对象> <目标对象>
git notes [--ref <注解引用>] append [--allow-empty] [-m <说明> | -F <文件> | (-c | -C) <对象>] [<对象>]
git notes [--ref <注解引用>] edit [--allow-empty] [<对象>]
git notes [--ref <注解引用>] show [<对象>]
git notes [--ref <注解引用>] merge [-v | -q] [-s <策略> ] <注解引用>
git notes merge --commit [-v | -q]
git notes merge --abort [-v | -q]
git notes [--ref <注解引用>] remove [<对象>...]
git notes [--ref <注解引用>] prune [-n] [-v]
git notes [--ref <注解引用>] get-ref

### range-diff

git range-diff [<选项>] <old-base>..<old-tip> <new-base>..<new-tip>
git range-diff [<选项>] <old-tip>...<new-tip>
git range-diff [<选项>] <base> <old-tip> <new-tip>

### rebase

git rebase [-i] [options] [--exec <cmd>] [--onto <newbase>] [<upstream>] [<branch>]
git rebase [-i] [options] [--exec <cmd>] [--onto <newbase>] --root [<branch>]
git rebase --continue | --abort | --skip | --edit-todo

### revert

git revert [<选项>] <提交号>...
git revert <子命令>
    --quit                终止反转或拣选操作
    --continue            继续反转或拣选操作
    --abort               取消反转或拣选操作
    -n, --no-commit       不要自动提交
    -e, --edit            编辑提交说明
    -s, --signoff         添加 Signed-off-by: 签名
    -m, --mainline        <父编号> 选择主干父提交编号
    --rerere-autoupdate   如果可能，重用冲突解决更新索引
    --strategy <策略>     合并策略
    -X, --strategy-option <选项> 合并策略的选项
    -S, --gpg-sign[=<key-id>] GPG 提交签名

### submodule

git submodule [--quiet] add [-b <branch>] [-f|--force] [--name <name>] [--reference <repository>] [--] <repository> [<path>]
git submodule [--quiet] status [--cached] [--recursive] [--] [<path>...]
git submodule [--quiet] init [--] [<path>...]
git submodule [--quiet] deinit [-f|--force] (--all| [--] <path>...)
git submodule [--quiet] update [--init] [--remote] [-N|--no-fetch] [-f|--force] [--checkout|--merge|--rebase] [--[no-]recommend-shallow] [--reference <repository>] [--recursive] [--] [<path>...]
git submodule [--quiet] summary [--cached|--files] [--summary-limit <n>] [commit] [--] [<path>...]
git submodule [--quiet] foreach [--recursive] <command>
git submodule [--quiet] sync [--recursive] [--] [<path>...]
git submodule [--quiet] absorbgitdirs [--] [<path>...]

### worktree

git worktree add [<选项>] <路径> [<提交>]
git worktree list [<选项>]
git worktree lock [<选项>] <路径>
git worktree move <工作区> <新路径>
git worktree prune [<选项>]
git worktree remove [<选项>] <工作区>
git worktree unlock <路径>

## Ancillary Commands / Manipulators

### reflog

    git reflog                          //查看版本历史记录(可获取commit id) HEAD@{number} number:移动到当前版本需要步数（该命令可用于查找commitId）

### remote

    git remote                                                      // 查看远程库信息，默认显示origin
    git remote -v                                                   // 查看远程链接状态 包括push 和fetch 地址
    git remote add aliasorigin <address>                            // 关联一个github远程仓库 <address>是仓库地址 
    git remote add aliasorigin "ssh格式地址"                         // 添加远程库
    git remote rm aliasorigin                                       // 删除远程地址
    git remote show <remote>                                        // 查看某一个远程仓库的更多信息
    git push -u origin master                                       // 关联远程仓库第一次提交的时候添加上-u参数，用于把本地以前的commit_log推送到远程库
    git push origin master                                          // 以后的推送就不需要-u参数
    git remote rename <old> <new>
    git remote remove <name>

    git remote add [-t <branch>] [-m <master>] [-f] [--[no-]tags] [--mirror=<fetch|push>] <name> <url>
    git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
    git remote set-branches [--add] <name> <branch>…​
    git remote get-url [--push] [--all] <name>
    git remote set-url [--push] <name> <newurl> [<oldurl>]
    git remote set-url --add [--push] <name> <newurl>
    git remote set-url --delete [--push] <name> <url>
    git remote [-v | --verbose] show [-n] <name>…​
    git remote prune [-n | --dry-run] <name>…​
    git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)…​]

### config

    git config user.name                                            // 查看用户名
    git config user.email                                           // 查看用户邮箱
    分全局设置、项目设置
    git config --global user.name "github`s Name"
    git config --global user.email "github@xx.com"
    git config --list
    git config --global http.postBuffer 524288000       // 调大git上传拉取大小
    git config --global credential.helper store         // 解决git每次提交推送都要输入密码
    git config --global alias.co checkout               // git 别名
    git config --global alias.br branch
    git config --global alias.unstage 'reset HEAD --'   
    git config --global alias.last 'log -1 HEAD'

### fast-export

### fast-import

### filter-branch

### mergetool


### pack-refs


### prune


### repack


### replace






