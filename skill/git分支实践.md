# 辅助分支实践

## Feature分支 方法一
feature 分支用来开发具体的功能，一般 fork 自 develop 分支，最终可能会合并到 develop 分支。

> 从 develop 分支建一个 feature 分支，并切换到 feature 分支
~~~
// 保证在最新的develop分支
$ git checkout develop
$ git pull origin develop

$ git checkout -b myfeature develop
~~~

> 合并 feature 分支到 develop。（防止feature分支合并到develop分支出现冲突，首先把最新的develop分支合并到本地）
~~~
// 切换 develop 分支,且保持版本最新
$ git checkout develop
$ git pull origin develop
// 合并 feature 分支
$ git checkout myfeature
$ git merge develop
~~~
> 若有冲突则解决冲突，commit提交
~~~
$ git commit -m -a "merge files"
~~~
> 合并feature到develop
~~~
$ git checkout develop
$ git merge --no-ff myfeature
$ git branch -d myfeature
$ git push origin develop
~~~
+ 参数 --no-ff，ff 是fast-forward 的意思,--no-ff就是禁用fast-forward。fast-forward知道哪些 commit 是某些 feature 相关的。
> 删除feature分支（若后续需要在此分支继续开发，则push origin）
~~~
$ git branch -d myfeature
~~~

## Feature分支 方法二
基于rebase合并分支。

> 从 develop 分支建一个 feature 分支，并切换到 feature 分支
~~~
// 保证在最新的develop分支
$ git checkout develop
$ git pull origin develop
// 新建feature分支
$ git checkout -b myfeature develop
~~~
> 修改代码
~~~
$ git add [file]
$ git commit -m ""
~~~
> 切换到develop分支,并保证其最新
~~~
$ git checkout develop
$ git pull origin develop
~~~
> 进行rebase
~~~
$ git checkout myfeature
$ git rebase develop
// 若代码冲突会停止rebase，需要解决冲突
$ git add [file]
$ git rebase --continue
~~~
> 合并feature到develop分支
~~~
$ git checkout develop
$ git pull origin develop
$ git merge myfeature
~~~
> 删除feature分支（若后续需要在此分支继续开发，则push origin）
~~~
$ git branch -d myfeature
~~~
+ git push --delete origin test (删除远端分支)  

## HotFix分支
用于修改master分支的bug

> 新建hotfix分支
~~~
$ git checkout -b hotfix-1.2.1 master
$ git commit -a -m "Bumped version number to 1.2.1"
~~~
> Fix bug
~~~
$ git commit -a -m "Fixed severe production problem"
~~~
> 将hotfix合并到master
~~~
$ git checkout master
$ git merge --no-ff hotfix-1.2.1
$ git tag -a 1.2.1
~~~
> hotfix 合并到 develop 分支（注意冲突的解决）
~~~
$ git checkout develop
$ git merge --no-ff hotfix-1.2.1
~~~
> 删除 hotfix 分支
~~~
$ git branch -d hotfix-1.2.1
~~~


