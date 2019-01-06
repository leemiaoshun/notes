### pr
> "Pull Request 是一种通知机制。你修改了他人的代码，将你的修改通知原来的作者，希望他合并你的修改，这就是 Pull Request。"

- 首先需要把别人的代码克隆到自己的仓库，==fork==


    1.目标仓库点击fork
    2.稍后在自己的仓库中点击 clone 到本地进行开发


- 上游建立连接，这里上游指的是一开始fork的那个项目源


    1.使用 git remote add upstream targetLinks 
    2.git remote -v 可以查看 已经关联的远程仓库
    
    
- 创建分支
    

    1.git checkout -b branchName // 也有检出的意思切换到分支XXX
    
- 查看文件修改


    1.git status
    
- 提交pr 
    
    1.远程仓库找到 ==New pull request== 选择 base 和compare 前者是目标分支 后者是自己要pr到目标的远程分支名
    2.点击 Create pull request


### git部分操作
```

1.git clone < url > // 目标仓库克隆代码

2.git init // 初始化本地git版本库

3.git status // 查看本地状态 修改状态

4.git add . //跟踪文件 参数可以设置指定文件名

5.git rm < fileName > // 删除文件

6.git rm –cached < filename > //停止跟踪但不删除

7.git commit -m 'commit message' // 提交到本地 已经暂存过的文件

8.git commit –amend //修改最后一次提交

9.git log // 查看提交历史

10.git log -p < fileName > //查看指定文件的提交历史

11.git branch // 显示本地的所有分支 -a （所有分支） -f (所有远程分支)

12.git checkout < branch/tag > //切换到指定分支或标签

13.git branch <new-branchName> // 创建新分支 -d (删除分支)

14.git merge < branch > //合并指定分支到当前分支

15.git remote // 列出所有远程主机

16.git remote -v //查看远程版本库信息

17.git remote show < remote > //查看指定远程版本库信息

18.git remote add < remote > < url > //添加远程版本库

19.git fetch < remote > //获取最新的远程更新

20.git pull < remote > < branch > //下载代码及快速合并

21.git pull < remote > < branch >:< local_branch > //下载代码与本地分支合并，默认采用merge模式合并

22.git pull –rebase < remote > < branch >:< local_branch >//下载代码与本地采用rebase模式合并

23.git push < remote > < branch > //上传代码及快速合并

24.git push < remote > < local_branch >:< remote_branch > //上传分支数据到远程

25.git push < remote > :< branch/tag-name > //删除远程分支或标签


```

