# Testing restore from backup

On the LXC container:
```
taha@hawalli:~
$ sudo systemctl stop apache2.service
```

Delete snipeit working directory:
```
taha@hawalli:~
$ sudo rm -rf /opt/snipeit/
```

Delete the database
```
taha@hawalli:~
$ sudo mariadb
Server version: 11.2.3-MariaDB-1:11.2.3+maria~ubu2204 mariadb.org binary distribution
MariaDB [(none)]> drop database snipeit;
Query OK, 50 rows affected (0.444 sec)
```

Restore using this role:
```
taha@asks2:/media/bay/taha/projects/ansible/dev/playbooks/luxor
(master *>) $ ansible-playbook playbook-containers.yml --ask-become-pass --limit snipeit -e "{ snipeit_restore: { overwrite: true, timestamp: '20240507T140902' }}"
```
