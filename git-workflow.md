
## create a topic branch and develop

``` export GIT_EDITOR=/usr/bin/vim
```

- clone a git workspace
``` git clone username@111.111.111.111:/opt/git/thegitworkspace
```
- show available branch
```
cd thegitworkspace
git branch -a
```
- create a new branch from develop
``` git checkout -b username_branch develop
```
- do work
- show things that have not been committed
``` git status
```
- add files to commit

```git add .```

- commit changes
``` git commit
```

- pull remote develop
``` git checkout develop && git pull origin develop
```
- switch to feature branch and rebase
``` git checkout username_branch && git rebase develop
```
- switch back to develop
``` git checkout develop
```
- merge the feature branch
```git merge --no-ff username_branch```
- delete feature branch
``` git branch -d username_branch```
