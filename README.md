# PHP7 Apache Ubuntu Setup
My workflow to get PHP7 running with apache on ubuntu 14 via php-fpm.

From an empty folder via an empty Ubuntu Vagrantbox Hyper-V to an Apache server thats running PHP7.
Warning: You'll need Hyper-V must be correctly installed and configured virtual switch
Warning: You'll need Vagrant and quite some bandwidth for this :)

Just clone this repository and run vagrant up in it (Go grab a coffe or something, this will take a while...):
Or download the repository in zip format and extract the folder where the vagrant will be initiated:
``root Windows C:/php7``
```bash
$ git clone https://github.com/Ferreiramg/php7_hyperv_apache.git
$ cd php7_hyperv_apache
```
# Manual Setup
## Change vagrantfile settings
```php
    :smb_username => 'user@windowsys.com',
    :smb_password => 'password'
``` 

## Inside our VM
### Installing php7

```bash
$ cd /var/www/php7_hyperv_apache
$ ./bootstrap.sh
```

Now we add the following somewhere into the /etc/apache2/apache2.conf file:
```
<IfModule mod_fastcgi.c>
        AddHandler php5-fcgi .php
        Action php5-fcgi /php5-fcgi
        Alias /php5-fcgi /usr/lib/cgi-bin/php5-fcgi
        FastCgiExternalServer /usr/lib/cgi-bin/php5-fcgi -host 127.0.0.1:9000 -pass-header Authorization
</IfModule>
```
But Apache thinks that /php5-fcgi is a directory it blocks it by default. So we have to delete the following block from the file:
```
<Directory />
        .........
</Directory>
```

Well now we just restart apache and are good to go:
```bash
$ sudo service apache2 restart
```
###Check on shell
```bash
$ php -v
```
If you now put a test.php file into /var/www/html with the following content:
```php
<?php

phpinfo();
```
You should now see the phpinfo page when you visit 192.168.7.8/test.php on your host pc.

If did something wrong or generally made and mistakes, please tell me, I'm still just learning all this stuff =D
