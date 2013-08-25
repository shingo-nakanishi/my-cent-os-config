## Make ssh file connect from Mac to Cent OS

### Document
http://tanaka.sakura.ad.jp/archives/001065.html

### in Mac
```
$ ssh-keygen
```

### in Cent OS
Paste public key to `~/.ssh/authorized_keys`

## Install zsh
### in Cent OS
check zsh isn't installed

```
$ cat /etc/shells
```

### only connect use public key
```
vim /etc/ssh/sshd_config

PermitRootLogin without-password
```

### Install zsh
```
$ yum install zsh
```

## Install my-config
Install https://github.com/shingo-nakanishi/my-config
### Make ssh file connect from Cent OS to Github
```
$ ssh-keygen
```

### Make ssh config
```
vim ~/.ssh/config

host github.com
   user git
   hostname github.com
   identityfile ~/.ssh/your_key
```
