## Better pull
```sh
# git stash
git pull --rebase <remote> <branch>
# git stash pop
```

若在pull之前有修改還不想commit，可以先commit後再reset

```sh
git add .
git commit -m "this commit will be removed"
git pull --rebase
git reset HEAD~1
```

## Commit

Amend author

```sh
git commit --amend --author='CodinCat <codincat@codeit.today>'
```

取消最新的commit，但保留修改的檔案
```sh
git reset HEAD~ --soft
```

完全刪除最新的commit
```sh
git reset HEAD~ --hard
```

## Revert
回復到某個commit（會產生一個新的revert commit）

```
git revert <commit>
```

取消掉特定的commit（會產生一個新的revert commit）

```
git revert --strategy resolve <commit>
```

## Branch

clone下來之後其實所有tag跟branch都有抓下來，只輸入`git branch`並不會顯示，用`git branch -a`就能看到，要切換到某個branch：
```
git checkout -b mybranch origin/mybranch
```

把最新的commit移到另一個branch

```sh
# 直接開一個新branch，它會有最新的commit
git branch branch2
# 再移掉master裡的commit就行
git reset HEAD~ --hard
git checkout branch2
```

把目前還沒stage也還沒commit的修改移到新的branch。直接checkout即可

```sh
git checkout -b mybranch
```

## Stash

```sh
git stash list
git stash apply stash@{2}
git stash drop stash@{0}
git stash --include-untracked # or git stash save -u
```

把目前還未commit的修改轉移到另一個branch，方法2

```sh
git stash
git checkout -b branch2
# or just checkout to an existing branch

git stash pop
# or use git stash apply
```

## Rebase & Merge

### Edit a specific commit

```sh
git rebase --interactive 'hashxxxxx^'
# edit...
git commit --amend
git rebase --continue
```

### 捨棄本地的修改，強制更新為remote版本

```sh
git fetch --all
git reset --hard origin/master
# git reset --hard <remote>/<branch>
```

![](http://i.imgur.com/IEAtoMD.png)
http://blog.sourcetreeapp.com/2012/08/21/merge-or-rebase/

## Tags
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

## Undo
取消目前還沒add(unstaged)的所有修改
```
git checkout -- .
```
https://github.com/blog/2019-how-to-undo-almost-anything-with-git

## Cheat Sheet
![](http://i.imgur.com/xBLgwXj.png)

------

## Set up SSH
```
ssh-keygen
ls -a ~/.ssh
> id_rsa  id_rsa.pub 
```
