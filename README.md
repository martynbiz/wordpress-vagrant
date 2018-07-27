# Wordpress Vagrant

This is a vagrant for Wordpress projects

## Installation

Firstly, ensure you have Vagrant installed, then:

```
git clone https://github.com/martynbiz/wordpress-vagrant myproject
cd myproject
cp VagrantFile.example VagrantFile
cp provision.sh.example provision.sh
```

Make whatever changes you need to VagrantFile and provision.sh (or leave as is for default configuration).

```
vagrant up
```

Once the Vagrant box is setup, download Wordpress files:

```
vagrant ssh
cd /var/www/uos-blog
wget http://wordpress.org/latest.tar.gz
tar xfz latest.tar.gz
mv wordpress/* ./
rmdir ./wordpress/
```

Create database:

```
mysql -u username -p

> create database blog;
```

Installation:

Go to url, step through installation process.
