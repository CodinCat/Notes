##Better pull
```
git pull --rebase <remote> <branch>
```

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

------

##Set up SSH
```
ssh-keygen
ls -a ~/.ssh
> id_rsa  id_rsa.pub 
```
