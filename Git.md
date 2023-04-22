## Git
    http://git-scm.com/docs/git-log

    ssh-keygen -t rsa -Cgit@github.com:xiannaipaofu/demo.git  //生成安全认证  
 
    git init  //初始化仓库

    git clone <仓库地址>  //克隆仓库
    git pull  //下载远程代码并合并
    git add <>  //添加文件到缓存区
    git commit -m 备注  //将缓存区内容添加到仓库中
    git push <仓库地址>  //上传远程代码并合并
    git publish  //上传仓库
    
    git status  //查看当前仓库状态是否有变更文件
    git log --oneline/--graph  //历史提交记录、历史记录何时出现分支合并
    git reset --soft/--hard <hash>  //不带参数(还原)、回退版本、回退并删除之前提交的所有版本

    git blame <file>  //查看指定文件修改记录
    git diff <>  //比较文件的不同
    git rm <>  //删除文件
    git mv <> <>  //移动文件

    git branch <>  //创建分支、-v查看所有分支、-d <> 删除分支
    git checkout <>  //切换分支、-b <> 创建并切换
    git merge <>  //合并分支

    git tag  //查看标签、-d <>删除标签
    git tag 别名 hash  //配置标签

    git cat-file -p hash  //

    git config --list  //显示当前git配置信息
    设置提交代码时的用户信息：
    git config --global user.name "runoob"
    git config --global user.email test@runoob.com

    gitee  //国内仓库
    IDEA  //集成仓库


