# git commands

easy way

```bash
git add *  
git commit -m "comment"  
git push origin master
```

```bash
# create & delete branch
git branch <branch name>        # create new branch <branch name>
git branch -d <branch name>     # delete branch
git checkout -b <branch name>   # create new branch and switch to the branch

# switch branch
git checkout <branch name>      # switch branch to <branch name>

# merge 
# before merge process commit master and another branch
git checkout master # switch to master branch
git merge <branch>  # merge branch
```

ref : https://rogerdudler.github.io/git-guide/index.ko.html