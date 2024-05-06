# Snipe-IT

Ansible role to install Snipe-IT asset manager.

> Snipe-IT is built on Laravel, [...] follows a standard Laravel MVC file structure.
> Within the Snipe-IT project, you'll see a `public` directory. That directory
> should be set as your document root.
> https://snipe-it.readme.io/docs/introduction

PHP >= 7.4 < v8.1.2 with the following extensions:
- JSON PHP Extension
- OpenSSL PHP Extension
- PDO PHP Extension
- `php-mbstring` Mbstring PHP Extension
- `php-tokenizer` Tokenizer PHP Extension
- `php-curl` cURL PHP Extension
- `php-mysql` MySQLi PHP Extension
- `php-ldap` LDAP PHP extension (only if using LDAP)
- `php-zip` PHPZIP PHP extension
- Fileinfo PHP extension
- `php-bcmath` PHP BCMath PHP extension
- `php-xml` PHP XML PHP extension
- PHP Sodium PHP Extension
- PHP Exif PHP Extension
+ `php-gd`

Composer `printf 'no\n'| sudo composer install --no-dev --prefer-source`
MySQL or MariaDB
GD Library (>=2.0) or Imagick PHP extension (>=6.3.8)
git



## Links and notes

> The upcoming v7 release of Snipe-IT will require **PHP 8.1** or greater.

+ https://github.com/snipe/snipe-it
+ https://snipe-it.readme.io/docs/common-issues
+ https://snipe-it.readme.io/docs/requirements
+ https://andrewdoering.org/blog/2016/asset-management-in-the-modern-age
+ https://github.com/glpi-project/glpi
+ https://github.com/kumarshreyansh/snipe-it-automation-using-ansible/blob/main/9-composer.sh
+ https://idroot.us/install-snipe-it-ubuntu-20-04


### Ansible roles

+ https://github.com/wiggels/ansible-role-snipe-it install, configure, and update a Snipe-IT server on Ubuntu 20/22
+ https://github.com/zubeirahamed/Ansible-snipe-it
+ https://github.com/howdycloudyarsh/SnipeIT-Ansible
+ https://github.com/GR360RY/snipeit-ansible deploy Snipe-IT on Debian and Ubuntu >12.04
+ https://github.com/cypherayan01/ansible-snipe-IT/tree/main/vagrant05/ansible/ansible-playbook/snipe-it last update 3 years ago
+ https://github.com/szulawski/snipe-it-ansible-role last update 5 years ago


### Handy commands

> Many issues can be resolved if you remember to run the following commands when
> you encounter weird errors:
> https://snipe-it.readme.io/docs/common-issues#quick-tip-handy-commands

```
composer dump-autoload
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan debugbar:clear
php artisan event:clear
php artisan view:clear
php artisan optimize:clear
php artisan clear-compiled
```

> These commands clear out cached service files that help speed up modern PHP applications
> but can also very occasionally be out of date, resulting in odd errors. These caches
> will be regenerated normally, so they can be cleared without repercussion.
> (You can also run `php update.php` from the Snipe-IT project directory to run
> these commands and other helpful clean-up commands all at once.)

Also be sure to delete the following files if they exist:
```
bootstrap/cache/compiled.php
bootstrap/cache/services.php
bootstrap/cache/config.php
```


### Sync with Unifi

+ https://github.com/RodneyLeeBrands/UnifiSnipeSync


### Sync with Netbox

+ https://github.com/derlucas/snipeit-netbox
+ https://www.thierolf.org/blog/2020/custom-links-in-netbox-for-snipe-it-asset-management
+ https://groups.google.com/g/netbox-discuss/c/Me_tqVgWj58
