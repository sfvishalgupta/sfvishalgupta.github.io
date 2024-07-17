# Git Clone

Clone with Below Command
```bash
ssh-agent bash -c 'ssh-add /somewhere/yourkey; git clone git@github.com:user/project.git'
```

Add below in .git/config
```yaml
sshCommand = ssh -i ~/.ssh/key
```