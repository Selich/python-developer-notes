## Git

 - https://gist.github.com/jedmao/5053440

Now, you can easily switch between branches with `git switch`:
```shell
git switch master
git switch develop
git switch feature_x
git config --global alias.sw 'switch'
git sw master
```


#### Switch to previous branch

```shell
git switch @{-1}

### [Undoing Commits](https://git-scm.com/docs/git-reset)

The following command will undo your most recent commit and put those changes back into staging, so you don't lose any work:
```shell
git reset --soft HEAD~1
```

The next one will completely delete the commit and throw away any changes. Be absolutely sure this is what you want:
```shell
git reset --hard HEAD~1
```

### [Squashing Commits](https://git-scm.com/docs/git-rebase)

Maybe you have 4 commits, but you haven't pushed anything yet and you want to put everything into one commit so your boss doesn't have to read a bunch of garbage during code review.
```shell
git rebase -i HEAD~4
```

### [Undo Last Push](https://git-scm.com/docs/git-reset)

Some would say this is bad practice. Once you push something you shouldn't overwrite those changes. Instead, you're supposed to create a new commit that reverts the changes in the last one. So, technically, you shouldn't do this, but... you can?
```shell
git reset --hard HEAD~1 && git push -f origin master
```



### [Rebasing](https://git-scm.com/docs/git-rebase)

Rebasing is a way of rewriting history. In place of merge, what this does is stacks your commits on top of commits that are already pushed up. In this case, you want to stack your commits on top of `origin/feature_x`:
```shell
git fetch origin
git rebase origin/feature_x
```

If you already have a local branch set to track `feature_x` then just do:
```shell
git rebase feature_x
```

Would you like to fetch, merge and then stack your changes on top, all in one shot? You can! If you have tracking setup on the current branch, just do:
```shell
git pull --rebase
```

Another great use of rebasing is just rewriting commit messages. To get an interactive text editor for the most recent commit, do:
```shell
git rebase -i HEAD~1
```

Now, you can replace "pick" with "r" and just change the commit message.


### [Stashing](https://git-scm.com/docs/git-stash)

Sometimes you need to stash your changes so you can be on a clean branch or maybe because you want to go back and try something before you make a commit with these changes. Here's how you do a stash:
```shell
git stash
```

Now, if you want to unstash those changes and bring them back into your working directory:
```shell
git stash pop
```

Or maybe you want to unstash your changes without popping them off the stack. In other words, you might want to apply these stashed changes multiple times. To do this:
```shell
git stash apply
```

For a list of stashes:
```shell
git stash list
```

And to apply a specific stash from that list (e.g., stash@{3}):
```shell
git stash apply stash@{3}
