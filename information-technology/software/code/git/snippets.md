*Mercurial ? Team Foundation what ? Helix who ? Crib hun !*

### Pull from master
```
git checkout my-branch

git fetch origin 

git merge origin/master
```


### List all branches
```
git branch -a
```

### Delete branch
```
git branch -d no-more-needed-branch
```

### New branch and checkout to it
```
git checkout -b some-branch
```

### New branch
```
git branch some-branch
```

### Commit
```
git commit -m "uhh, changed stuff"
```

### You mighta messed that up
```
//changed files
git status
```

### Kickoff
```
git init
```

---

## Undo commit

### If not pushed

#### Keep the changes:
```
git reset --soft HEAD~1

```

#### Destroy the changes
```
git reset --hard HEAD~1

```

### If pushed

```
# get the hash of your commit
git log -p 

git revert [commit hash]
# git revert 0a3dbc774ea29bfd68fe55caf1ade33dba1bda35
```

---
