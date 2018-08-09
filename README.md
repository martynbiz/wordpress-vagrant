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

## Optional changes

Make whatever changes you need to VagrantFile and provision.sh (or leave as is for
default configuration). Below are some recommended/optional changes:

VagrantFile

The following is what IP address is assigned to the box.

```
config.vm.network "private_network", ip: "192.168.33.60"
```

It can be left as is, but remember to add blog.vagrant to your /etc/hosts file.
For example:

If this domain ought to be different, set in the hosts file and update the Apache
VirtualHost config in provision.sh too.

provision.sh

This script will install wp-cli so we can install and setup our new installation
from the command line. This is also really useful when we `vagrant ssh`.

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

Now that provision and vagrantfile are ready, start up the vagrant instance:

```
vagrant up
```

## What next?

Login to wp-admin

Unless you've change the `wp install` command in provision, your can login with supervisor/strongpassword.

Choose/download a theme, create menus, create posts etc

TODO
* hosts, etc .. OR configure to /vagrant ; 8080
* media file
* allow media files to be uploaded via admin ui
