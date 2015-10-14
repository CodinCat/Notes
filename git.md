##Better pull
```
git pull --rebase <remote> <branch>
```

##Rebase & Merge
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
