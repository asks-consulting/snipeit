# Snipe-IT

Ansible role to install and configure Snipe-IT asset manager.

> Snipe-IT is built on Laravel, [...] follows a standard Laravel MVC file structure.
> Within the Snipe-IT project, you'll see a `public` directory. That directory
> should be set as your document root.
> https://snipe-it.readme.io/docs/introduction


For reference, the Apache vhost on the reverse proxy:
```
<VirtualHost *:80>
   ServerAdmin {{ vhost.email }}
   ServerName {{ vhost.domain }}

   Redirect permanent / https://{{ vhost.domain }}/

   ErrorLog ${APACHE_LOG_DIR}/{{ vhost.domain }}_error.log
   CustomLog ${APACHE_LOG_DIR}/{{ vhost.domain }}_access.log combined
</VirtualHost>

<VirtualHost *:443>
   ServerAdmin {{ vhost.email }}
   ServerName {{ vhost.domain }}

   ProxyPreserveHost On
   ProxyPass / http://{{ vhost.ip }}/
   ProxyPassReverse / http://{{ vhost.ip }}/
   RequestHeader set X-Forwarded-Proto "https"

   SSLEngine on
   SSLCertificateKeyFile   /etc/letsencrypt/live/{{ vhost.domain }}/privkey.pem
   SSLCertificateFile      /etc/letsencrypt/live/{{ vhost.domain }}/cert.pem
   SSLCertificateChainFile /etc/letsencrypt/live/{{ vhost.domain }}/chain.pem

   ErrorLog ${APACHE_LOG_DIR}/{{ vhost.domain }}_error.log
   CustomLog ${APACHE_LOG_DIR}/{{ vhost.domain }}_access.log combined
</VirtualHost>
```

## Known issue

Mail does not work to my mailserver which uses `starttls`. Not sure why.
Seems Snipe-IT does not support/allow `starttls` despite both `openssl` and
`telnet` on the same host connecting fine to the mailserver.
The log in `/opt/snipeit/storage/logs/laravel.log` appears to produce output, but
I find it practically impossible to understand it (no timestamps, weird syntax).

In the GUI it just says `Mail could not be sent`, and `No additional error message provided`.
I guess I can live without Snipe-IT's emails.



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

+ https://github.com/snipe/snipe-it/blob/master/ansible/ubuntu/vagrant_playbook.yml
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
