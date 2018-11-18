# VPS Config

```sh
yum update -y
yum install httpd mariadb mariadb-server php php-mysql -y
systemctl start httpd.service
systemctl start mariadb.service
systemctl enable httpd.service
systemctl enable mariadb.service
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload
```

```sh
mysql_secure_installation
cp /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.bak
sed -i -e 's/DirectoryIndex index.html/DirectoryIndex index.php index.html/g' /etc/httpd/conf/httpd.conf
systemctl restart httpd.service
```

```sh
adduser ...
passwd -l ...
usermod -s /sbin/nologin ...

chown apache:apache -R /home/

cd /home/
find . -type f -exec chmod 0644 {} \;
find . -type d -exec chmod 0755 {} \;


chcon -t httpd_sys_content_t /home/ -R
chcon -t httpd_sys_rw_content_t /home/ -R
```

```sh
mkdir /etc/httpd/sites-available
mkdir /etc/httpd/sites-enabled

vi /etc/httpd/conf/httpd.conf =>[last line]=> IncludeOptional sites-enabled/*.conf

vi /etc/httpd/sites-available/mohsenshabanian.conf 

<VirtualHost *:80>
  ServerName www.mohsenshabanian.com
  ServerAlias mohsenshabanian.com
  DocumentRoot /home/mohsenshabanian/public_html 
  ErrorLog /home/mohsenshabanian/error.log 
  CustomLog /home/mohsenshabanian/requests.log combined 
</VirtualHost>

ln -s /etc/httpd/sites-available/itse.conf /etc/httpd/sites-enabled/itse.conf
```

```sh
vi /etc/hosts
```

---------------------------------------------

## Laravel Config

```sh
chown apache:apache -R /home/
```

install composer (from site)

```sh
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
mv composer.phar /usr/local/bin/composer
```

### install php7.2

```sh
yum-config-manager --enable remi-php72
yum install php72
yum install php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysql -y

systemctl start php72-php-fpm.service
systemctl status php72-php-fpm.service
systemctl enable php72-php-fpm.service
```

install php-zip

```sh
yum-config-manager --enable remi-php72
yum install php php-fpm php-common php-xml php-mbstring php-json php-zip
```

add to mysite.conf

```conf
<Directory />
    AllowOverride ALL
</Directory>
```

after that

```sh
systemctl restart httpd
```

disable selinux

```sh
vi /etc/sysconfig/selinux => SELINUX=disabled
reboot
```