#  Git 简单操作

> ### 只有先从远方数据库同步到本地才可以在提交没有冲突，注意 .git所在的文件夹！！



> 新建立的数据库，在GitHub上的workspace这个仓库还是空的，需要建立远方和本地的联系，把本地的内容推送到GitHub仓库
>
> > git remote add origin git@github.com:windrise/workspace.git
> >
> > __注意__： 添加后,远程数据库的名字就是__origin__ ，
>
> 下一步就可以把本地库的所有内容推送到远程库 上：
>
> > git add .   #或者 git add README.md   把要push的文件添加到.git目录
> >
> > git commit -m "描述提交"    # 提交的描述
> >
> > git push -u origin master    # 远方库 master或者test分支，取决你当前所在的库
> >
> > git push origin master      # 把本地master分支的最新修改推送到github（-f 强制）

### 现在远程库已经准备好了，下一步就是用命令克隆一个本地块



> git clone git@github.com:windrise/workspace.git



> git branch test   # 创建test分支
>
> git checkout test  # 切换分支
>
> git checkout -b test     # 创建并切换到test分支
>
> git branch -a  # 显示当前所有分支
>
> git status 查看状态
>
> 如果push出现错误，强制push
>
> git push -f 
>
> 