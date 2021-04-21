# WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
### Create an AWS account
### Create an EC2 Instance
### Provison an Ubuntu Server
### Connect to the Ec2 Instance
### Download a private key from the instance while provisioning the Server
### Convert the file to a .ppk file extension with the help of puttyGen
## Checklist

*[x] Public IP address

*[x] ‘ubuntu’ as user

*[x] .ppk private key file
### Retrieve the Public IP address to your instance
### Copy EC2 Public IP address
### Paste the public IP, load the private key on putty and connect.
### Install Apache and Update the Firewall
``` bash
#update a list of packages in package manager
$ sudo apt update
#run apache2 package installation
$ sudo apt install apache2
```
### Verify that apache2 is running as a Service in our OS

``` bash
$ sudo systemctl status apache2
```
### Edit Inbound Rules and add a rule to EC2 configuration to open inbound connection through port 80
### check how we can access it locally in our Ubuntu shell

``` bash
$ curl http://localhost:80
```
### Checked with my public ip address on the browser <Public-IP-Address>
![image](https://user-images.githubusercontent.com/41236641/115602134-7f74e380-a2d6-11eb-8c2f-879bd7a702a8.png)

### Install Mysql
``` bash
$ sudo apt install mysql-server
$ sudo mysql_secure_installation
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?
Press y|Y for Yes, any other key for No:
```
### Enabled Password 
### Test Login to Mysql
``` bash
$ sudo mysql
```
### Exit Mysql
```bash
mysql> exit
```
### Install Php
``` bash
$ sudo apt install php libapache2-mod-php php-mysql
```
### Confirm Version
``` bash
php-v
 ```
 ### Create a Virtual Host for your Website using Apache
 ### Create the directory for projectlamp using ‘mkdir’ command
 ```bash
 $ sudo mkdir /var/www/projectlamp
 ```
 ### assign ownership of the directory with the $USER environment variable, which will reference your current system user
 ``` bash
 $ sudo chown -R $USER:$USER /var/www/projectlamp
 ```
 ### create and open a new configuration file in Apache’s sites-available directory
 ```bash
 $ sudo vi /etc/apache2/sites-available/projectlamp.conf
 ```
 ### This will create a new blank file and paste in the bare-bones configuration
 ```bash
 <VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost> 
```
### show the new file in the sites-available directory
```bash
$ sudo ls /etc/apache2/sites-available
000-default.conf  default-ssl.conf  projectlamp.conf
```
###  Enable the new virtual host
```bash
$ sudo a2ensite projectlamp
```
### disable the default website that comes installed with Apache
```bash
$ sudo a2dissite 000-default
```
### To check for Synthax errors
```bash
$ sudo apache2ctl configtest
```
### reload apache
```bash
$ sudo systemctl reload apache2
```
### To Create an index.html file in the web root /var/www/projectlamp so that we can test the virtual host
```bash
sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html

```
### Check the website URL using IP address

```bash
web root /var/www/projectlamp
```

### Enable PHP on the website
### change hierachy of default Directory index.
```bash
sudo vim /etc/apache2/mods-enabled/dir.conf
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
### reload apache
```bash
$ sudo systemctl reload apache2
```
### Create a new file named index.php inside your custom web root folder
``` bash
$ vim /var/www/projectlamp/index.php
```

### Add a valid php code detaling the about page
```bash
<?php
phpinfo();
```

![image](https://user-images.githubusercontent.com/41236641/115624311-5e21f080-a2f2-11eb-80a7-c79dbe15c66d.png)
## Project Completed
