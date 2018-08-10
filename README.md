# Wordpress Vagrant

This is a vagrant for Wordpress projects

## Installation

Firstly, ensure you have Vagrant installed, then:

```
git clone https://github.com/martynbiz/wordpress-vagrant myproject
cd myproject
cp Vagrantfile.example Vagrantfile
cp provision.sh.example provision.sh
```

Add the blog.vagrant domain to the /etc/hosts file:

```
192.168.33.60	blog.vagrant
```

This domain can be changed if preferred. See optional changes below.

## Optional changes

Make whatever changes you need to VagrantFile and provision.sh (or leave as is for
default configuration). Below are some recommended/optional changes:

### Change network IP and/or domain

The are a couple changes required:

VagrantFile

```
config.vm.network "private_network", ip: "<new IP address>"
```

This new IP address must match the IP address in /etc/hosts.

Also, if changing the domain, find instances of blog.vagrant in provision.sh file
and change those to the new domain if that has changed too.

### Seeding database on vagrant up

Insert posts, pages, categories etc each time so the blog has content to work with
even if just in development.

provision.sh

This script will install wp-cli so we can install and setup our new installation
from the command line. This is also a really useful tool when we `vagrant ssh`.

Ensure these are placed at the end of the shell script:

Edit this line with your own user/pw/email for the admin user

```
# edit this line...
wp core install --url='<Blog URL>' --title='<Blog name>' --admin_user=<Admin user> --admin_password=<Admin user> --admin_email=<Admin email> --skip-email
```

Add some new lines to create posts/categories for testing in dev. These will be
created on a new vagrant up:

```
# Create posts
wp post create ./lipsum.txt --post_title='Keep calm this summer' --post_status=publish

# Create category
wp term create category "News" --description="News"
```

## Run vagrant

Now that provision.sh and Vagrantfile are ready, start up the vagrant instance:

```
vagrant up
```

It should now be possible to view the new blog in the browser with the domain used.
This will be http://blog.vagrant if unchanged.

## What now?

Unless you've change the `wp install` command in provision, your can login to wp-admin
with supervisor/strongpassword. Choose/download a theme, create menus, create posts etc
