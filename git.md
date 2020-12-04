## Rebasing

REbasing copies commits from one branch to another so the git commit history looks linear.
So if you have a repo with commit C1 on main, then a branch myBranch with commit C2, and a separate commit C3 on main.
With myBranch checked out, doing `git rebase main` will copy C3 into myBranch.

How do you then get that back into main? 

## Traversing the tree
To go up one commit use `^` eg. `git checkout HEAD^` or `git checkout myBranch^`
To go up `n` commits use `~` e.g. `git checkout HEAD~2`

## Moving a branch to a different commit
`git branch <target commit> -f myBranch`

## Reversing a commit
We can move back in time with `git reset <commit to go back to>`
So to undo the most recent commit `git reset HEAD~1`
Only do that if the commits haven't been pushed to the remote

If dealing with a remote then use `git revert <the commit to undo>`
So to undo the most recent commit `git revert HEAD`

## Cherry Picking
If you want to copy over one or more commits from another branch(es) you can use `git cherrypick`
Make sure you are checked out on the branch you want to apply the commits to. Then run `git cherrypick <space separated list of commit hashes>`. This will bring over each of those commits on top of your branch. Each one will get its own new commit

## Interactive re-basing
You can use `git rebase -i <point to go back to>`
This allows you to essentially replay the commits between where you are now and the point in the past you specify. From there you can include or exclude commits and re-order them. I guess this essentially rewrites history, giving a new set of potentially re-ordered and reduced commits.

You can also squash commits doing this too. I guess this should only be done locally (maybe it can be done on a private remote branch)



#git #onboarding