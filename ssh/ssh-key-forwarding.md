# SSH Key Forwarding
_02/10/2016_

SSH Key Forwarding allows one to use SSH keys on their local machine to connect
to a remote server via an intermediary.  This provides extra security as SSH keys
do not need to be kept on the server.  This is helpful for accessing servers that
sit behind a NAT, etc.

```bash
# Add the SSH key that you use to connect to remote machine to the SSH agent
ssh-add ~/.ssh/remote/key/here.pem -K # -K flag adds key to OS X keychain

# Open an SSH connection to the intermediary server (the NAT)
ssh -i ~/.ssh/intermediary/key/here.pem -A user@intermediary.server.host

# Once connected to intermediary server, your local keys are available
ssh user@remote.server.host
```
