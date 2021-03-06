## Summary
magento2box is a Vagrant image based on Rasmus Lerdorf's [php7dev](https://github.com/rlerdorf/php7dev) Vagrant image. It comes preconfigured with PHP 7, Nginx, MySQL 5.6 and a base install of the Magento 2.

## Installation

Download and install [Virtualbox](https://www.virtualbox.org/wiki/Downloads)

Download and install [Vagrant](https://www.vagrantup.com/downloads.html)

```
$ git clone git@github.com:RMcLeod79/magento2dev.git
```
Now copy magento2.box into magento2dev

```
$ cd magento2dev
...
$ ./setup.sh
...
$ vagrant up
...
$ vagrant ssh
...
$ ./install.sh
```

Add this to your hosts file:

```
192.168.7.7 magento2.dev
```

There are also various vagrant plugins that can help you update your dns. See [local-domain-resolution](https://github.com/mitchellh/vagrant/wiki/Available-Vagrant-Plugins#local-domain-resolution).  

At this point you should be able to point your  browser at:

```
http://magento2.dev/
```

and it should show the Magento 2 Store home page.


## Server Setup
The Magento2 files can be found in ./htdocs these are shared to /var/www/magento2 on the guest machine

All passwords on the server (sudo, MySQL root etc.) are vagrant

## Magento 2 bug
When you try to login to the admin you will get an error, this error is something to do with config cache. To get round it:
```
$ vagrant ssh
...
$ cd /var/www/magento2
...
$ rm -rf var/cache
```
Now refresh the admin page and you will see the dashboard. Try navigating to System -> Cache and you will get the same error again. Remove the cache folder again and refresh you will now see the cache settings, disable config cache and the problem goes away.

The problem is to do with when Magento tries to unserialize the cache data, feel free to find a fix and PR it to [Magento](https://github.com/magento/magento2)