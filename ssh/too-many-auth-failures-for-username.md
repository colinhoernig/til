# Fixing `Too many authentication failures for x`
_03/08/2016_

Have you ever attempted to make an SSH connection to a remote server only to
receive an error stating `Too many authentication failures for {username}`?

The reason this issue happens is because SSH attempts to try all of the keys
in the SSH agent before attempting the key provided by the `-i` flag or
`IdentityFile` statement within your SSH configuration file.

Do not fear, there are a few very simple solutions.  The easiest solution is to
edit your SSH configuration to specify `IdentitiesOnly yes` globally.  To do so,
edit `~/.ssh/config` and add the statements below:

```
Host *
IdentitiesOnly yes
```

By adding `IdentitiesOnly yes` for all hosts, SSH will use the key you specify
via either the `-i your-key-here.pem` flag at runtime or the
`IdentityFile your-key-here.pem` statement within the specific host of your SSH
configuration.

```
Host your.host.com
HostName your-fqdn.com # fully qualified hostname
IdentityFile "~/.ssh/id_rsa" # your SSH private key
```
