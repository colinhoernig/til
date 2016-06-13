# Handy Git Commands
_06/13/2016_

Here are a few commands that I've found handy.

* List all branches and the remote branches that they track ([SO question](http://stackoverflow.com/questions/4950725/how-do-i-get-git-to-show-me-which-branches-are-tracking-what))

```bash
git branch -vv # double verbose flag
```

* Generate a git patch for a specific commit ([SO question](http://stackoverflow.com/questions/6658313/generate-a-git-patch-for-a-specific-commit/6658352#6658352))

```bash
git format-patch -1 <sha>
```
