## Document
http://tanaka.sakura.ad.jp/archives/001065.html


## Make ssh file connect from Mac to Cent OS
### in Mac
```
$ ssh-keygen
```

### in Cent OS
Paste public key to `~/.ssh/authorized_keys`

### Only connect use public key
Edit file `/etc/ssh/sshd_config`
```
PermitRootLogin without-password
PasswordAuthentication no
```

## Install zsh
### in Cent OS
check zsh isn't installed

```
$ cat /etc/shells
```

### Install zsh
```
$ yum install zsh
```

## Config SSH (You can git clone from GitHub)
### Make ssh file connect from Cent OS to Github
```
$ ssh-keygen
```
and register yourkey to GitHub.

### Make ssh config
```
vim ~/.ssh/config

host github.com
   user git
   hostname github.com
   identityfile ~/.ssh/your_key
```

### ssh agent
```
$ eval `ssh-agent -s`
$ ssh-add ~/.ssh/your_key
```

## Install my-config
Install https://github.com/shingo-nakanishi/my-config

## Install Redmine
### Document
http://www.redmine.org/projects/redmine/wiki/Redmine_on_CentOS_installation_HOWTO

```
$ yum -y install zlib-devel curl-devel openssl-devel httpd-devel apr-devel apr-util-devel mysql-devel
$ cd ~
$ yum install gcc-c++
$ git clone git@github.com:redmine/redmine.git
$ gem install passenger
$ mkdir /var/www/redmine
$ cp -av redmine-1.3.2/* /var/www/redmine
$ yum install mysql-server
$ chkconfig mysqld on
$ service mysqld start
$ /usr/bin/mysql_secure_installation
$ mysql -u root -p
$ mysql> create database redmine character set utf8;
$ mysql> create user 'redmine'@'localhost' identified by 'my_password';
$ mysql> grant all privileges on redmine.* to 'redmine'@'localhost';
$ mysql> \q
$ cd /var/www/redmine/config
$ cp database.yml.example database.yml
$ gem install bundler
$ cd /var/www/redmine
$ b-install-local
$ RAILS_ENV=production bundle exec rake generate_secret_token
$ RAILS_ENV=production bundle exec rake db:migrate
$ RAILS_ENV=production bundle exec rake redmine:load_default_data
$ cd /var/www/redmine/public
$ cp htaccess.fcgi.example .htaccess
$ cd /var/www
$ chown -R apache:apache redmine
$ chmod -R 755 redmine
$ b-rails s -e production
```

If got error `b-install-local`
install ImageMagick-devel
```
$ yum install ImageMagick-devel
```
