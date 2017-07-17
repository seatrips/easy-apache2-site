# Easy-apache2-site
Easy dummy guide for new delegates to make a website on a vps 

# What you need to do after prepairing the vps with a user

## 1- Make a domain for your server and edit hostname to:

YOURSERVERDOMAIN

## 2- Install apache2
```
sudo apt-get install apache2
```
## 3- Install ssl certificate
```
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install certbot 
sudo certbot certonly --standalone -d YOURSERVERDOMAIN -d YOURSERVERDOMAIN
```
## 4- Activate ssl module
```
sudo a2enmod ssl
```

## 5- Edit config file of enabled site in apache
sudo nano /etc/apache2/sites-enabled/000-default.conf

## 6- Put this in your config after deleting what was already in there

```
NameVirtualHost *:80
<VirtualHost *:80>
   ServerName YOUR SERVER DOMAIN
   DocumentRoot /usr/local/apache2/htdocs
   Redirect permanent / https://YOURSERVERDOMAIN/
</VirtualHost>

<VirtualHost *:443>
                ServerAdmin webmaster@localhost
                DocumentRoot /var/www/html
                ErrorLog ${APACHE_LOG_DIR}/error.log
                CustomLog ${APACHE_LOG_DIR}/access.log combined
                SSLEngine on
                SSLCertificateFile /etc/letsencrypt/live/YOURSERVERDOMAIN/fullchain.pem
                SSLCertificateKeyFile /etc/letsencrypt/live/YOURSERVERDOMAIN/privkey.pem
</VirtualHost>
```

## 7- Restart Apache2 to make changes active
```
sudo service apache2 restart
```

## Now you should see the index.html thats in your /var/www/html folder when you go to http://YOURDOMAIN and it should redirect to https://YOURDOMAIN
