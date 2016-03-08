# Remote Git operations fail after updating SSH config to use IdentitiesOnly
_03/08/2016_

After updating your [SSH configuration to use IdentitiesOnly](/ssh/too-many-auth-failures-for-username.md), one may run into
an issue where remote Git operations fail:

```
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

The reason for permission denied error is because SSH does not know which
`IdentityFile` to use for the remote host.  This is easily resolved by editing
your SSH configuration to explicitly specify which private key to use for the
remote repositories host.

```
Host github.com
HostName github.com
IdentityFile "~/.ssh/id_rsa"
```
