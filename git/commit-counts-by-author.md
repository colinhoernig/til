# View Commit Counts by Author
_04/02/2016_

Sometimes it's interesting to see the number of commits in a repository per author.
Git has a built in `shortlog` command that makes this data easy to retreive.

```bash
git shortlog -s -n
```

`-s` - Squash commit messages into number of commits
`-n` - Order by commit count, descending
