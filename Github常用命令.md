### Github常用命令

#### PULL

>  当本地的当前分支不是local_branch，将远程分支拉取到指定本地分支：`git pull origin <remote_branch>：<local_branch>`
>
> 在当前分支上进行同步操作，将指定远程分支同步到当前本地分支:
>
> `git pull origin <remote_branch>`
>
> 本地分支已经和想要拉取的分支建立了“关联”关系；拉取所有远程分支的新版本"坐标"，并同步当前分支的本地代码：`git pull`
>
> 查看分支关联信息：git branch -vv
>
> 配置本地分支与远程分支三种方法(**注：默认配置下，提交时本地分支需和远程分支同名**)
>
> 1. 检出时建立关联关系：`git checkout -b dev origin/dev`
>    当我们检查时，git会自动为我们检出的分支和远程分支建立关联关系；
> 2. 提交时配置关联关系：`git push -u origin <remote_branch>`或`git push --set-upstream origin <remote_branch>`
> 3. 更改git/config文件：`git branch --set-upstream-to=<remote_branch>`

#### 推送

> 推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上:
>
> `git push origin master`
>
> 推送其他分支：`git push origin dev`
>
>  - `master`分支是主分支，因此要时刻与远程同步；
>  - `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
>  - `bug`分支只用于在本地修复`bug`，就没必要推到远程了，除非老板要看看你每周到底修复了几个`bug`；
>  - `feature`分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

#### 分支(Branch)

> 查看分支：`git branch`
>
> 创建分支：`git branch <name>`
>
> 切换分支：`git checkout <name>`
>
> 创建+切换分支：`git checkout -b <name>`
>
> 合并某分支到当前分支：`git merge <name>`
>
> 删除分支：`git branch -d <name>`
>
> 强行删除未merge的 分支： `git branch -D <name>`
>
> 看到分支合并情况：`git log --graph --pretty=oneline --abbrev-commit`

#### 储藏（Stashing)

> 当你正在进行项目中某一部分的工作，里面的东西处于一个比较杂乱的状态，而你想转到其他分支上进行一些工作。问题是，你不想提交进行了一半的工作，否则以后你无法回到这个工作点。解决这个问题的办法就是`git stash`命令。——**注意：必须在stage即git add**
>
> 储藏：`git stash`
>
> 列出现有储藏：`git stash list`
>
> 应用储藏： `git stash apply` 恢复最近一次stash
>
> ​			`git stash apply stash@{n}`恢复指定某次stash
>
> 恢复后删除：`git stash drop`删除恢复后的stash
>
> 恢复最近+删除：`git stash pop`

#### 远程

> 查看远程库信息： `git remote `
>
> 查看远程库更详细的信息： `git remote -v `
>
> 抓取分支：	
>
> 1.  `git clone XXX`
>
>              		           2. 创建远程`origin`的`dev`分支到本地` git checkout -b dev origin/dev`

#### 多人协作

> - 查看远程库信息，使用`git remote -v`；
> - 本地新建的分支如果不推送到远程，对其他人就是不可见的；
> - 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
> - 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
> - 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
> - 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

#### 标签管理

> - 切换到需要打标签的分支上，输入：`git tag v1.0`
>
> - 查看标签：`git tag`
> - 通过commit id打标签：`git tag v1.0 <commid id>`
> - 创建带有说明的标签：`git tag -a <tagname> -m "blablabla..."`
> - 删除标签：`git tag -d <tagname>`
>
> **因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。**
>
> - 命令`git push origin <tagname>`可以推送一个本地标签；
> - 命令`git push origin --tags`可以推送全部未推送过的本地标签；
> - 命令`git tag -d <tagname>`可以删除一个本地标签；
> - 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

#### 忽略特殊文件

> 在Git工作区的根目录下创建一个特殊的`.gitignore`文件
>
> 例如：
>
> ```.git
> # Windows:
> Thumbs.db
> ehthumbs.db
> Desktop.ini
> 
> # Python:
> *.py[cod]
> *.so
> *.egg
> *.egg-info
> dist
> build
> 
> # My configurations:
> db.ini
> deploy_key_rsa
> 
> ```
>
> 忽略以后强制添加：`git add -f <filename>`
>
> 检查.gitignore文件：`git check-ignore -v <filename>   `

#### Rebase

> 详见http://gitbook.liuhui998.com/4_2.html