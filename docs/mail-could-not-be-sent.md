# "Mail could not be sent" on pre-flight setup screen


We have `openssl` on the host, and can connect to the mail server:
```
taha@hawalli:/opt/snipeit
$ openssl s_client -connect mail.asks.se:587 -starttls smtp
```
(output redacted above, but it works).

+ https://www.saotn.org/test-smtp-authentication-starttls

Telnet also connects successfully to our mail server:
```
$ telnet mail.asks.se 587
Trying 157.90.146.27...
Connected to mail.asks.se.
Escape character is '^]'.
220 mail.asks.se ESMTP Postfix
```

Apparently we cannot set `starttls` in the env `MAIL_ENCRYPTION`, and none
of those listed in `php.ini` worked either. I am stumped.

After changing `.env` you should clear cache
```
sudo -u www-data php artisan config:clear
sudo -u www-data php artisan config:cache
```
then restart the webserver for good measure:
```
sudo systemctl restart apache2.service
```

+ https://github.com/snipe/snipe-it/discussions/14041
+ https://stackoverflow.com/questions/5265692/smtp-server-response-530-5-7-0-must-issue-a-starttls-command-first
+ https://github.com/snipe/snipe-it/issues/8231
+ https://github.com/snipe/snipe-it/issues/10039
+ https://snipe-it.readme.io/docs/configuration#required-outgoing-mail-settings
+ https://github.com/thilinadias/thilinadias/discussions/1
