##Better pull
```
git pull --rebase <remote> <branch>
```

若在pull之前有修改還不想commit，可以先commit後再reset

```sh
git add .
git commit -m "this commit will be removed"
git pull --rebase
git reset HEAD~1
```

##Branch
clone下來之後其實所有tag跟branch都有抓下來，只輸入`git branch`並不會顯示，用`git branch -a`就能看到，要切換到某個branch：
```
git checkout -b mybranch origin/mybranch
```

##Commit
Amend author
```sh
git commit --amend --author='CodinCat <codincat@codeit.today>'
```

##Revert
回復到某個commit（會產生一個新的revert commit）
```
git revert <commit>
```

##Stash

```sh
git stash list
git stash apply stash@{2}
git stash drop stash@{0}
git stash --include-untracked # or git stash save -u
```

把目前還未commit的修改轉移到另一個branch

```sh
git stash
git checkout -b branch2
# or just checkout to an existing branch

git stash pop
# or use git stash apply
```

##Rebase & Merge

###捨棄本地的修改，強制更新為remote版本

```sh
git fetch --all
git reset --hard origin/master
# git reset --hard <remote>/<branch>
```

![](http://i.imgur.com/IEAtoMD.png)
http://blog.sourcetreeapp.com/2012/08/21/merge-or-rebase/

##Tags
給一個commit標上tag
```
git tag -a v1.0 <commit hash>
```

List tags
```
git tag -l
git tag -l 'v1.*'
```

Push all tags
```
git push origin --tags
```

##Undo
取消目前還沒add(unstaged)的所有修改
```
git checkout -- .
```
https://github.com/blog/2019-how-to-undo-almost-anything-with-git

##Cheat Sheet
![](http://i.imgur.com/xBLgwXj.png)

------

##Set up SSH
```
ssh-keygen
ls -a ~/.ssh
> id_rsa  id_rsa.pub 
```
