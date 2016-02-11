# Changing Repository Root
_02/10/2016_

If you've initialized a Git repo in the wrong directory and want to move it
without losing history, this is an easy way to restructure.

```bash
# Move the .git folder to the proper location
mv .git ../

# Reinitialize repo in proper location
cd ..
git init

# Add all files, commit, and push
git add .
git commit -am "Restructuring..."
git push origin master
```

_Originally seen on [StackOverflow](http://stackoverflow.com/a/17622123/2824419)_
