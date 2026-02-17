# Setup git credentials

~/.ssh/config:

```
Host github-phas13
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_phas13
    IdentitiesOnly yes
```

Run in the cloned git repo:

```
cd <PATH>/phas13/argentarius
git remote set-url origin git@github-phas13:phas13/argentarius.git
```
