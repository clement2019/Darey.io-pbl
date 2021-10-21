      PROJECT1 : WEB STACK IMPLEMENTATION   (LAMP STACK) IN AWS
I started this project by first creating a lamp-stack web server in Aws in my availability zone eu-west 2a, configured the security group with the necessary configuration settings 
SSH on port:22 and HTTP on port :80 thereby creating the necessity FIREWALL.
 I created my private key to be able to connect to my EC2 instance and with the help of the key I was able to use (SSH client) connection to connect to my instance using Gitbash

INSTALLED APPACHE2 

Installed Apache2 using the command below
Sudo apt install appeche2

![image](https://user-images.githubusercontent.com/55473846/138329103-8ea0f79a-4aec-4429-b285-a881178d6e7c.png)

I render the webserver through port: 80 which is the default port that web browsers to have access to the web pages 
To confirm the apache2 is working

![image](https://user-images.githubusercontent.com/55473846/138329573-a37b337b-a923-4767-a37b-756f71e973da.png)

I try to see if I can now access ubuntu locally on my system

curl http://localhost:80

![image](https://user-images.githubusercontent.com/55473846/138329943-6d3a8d2d-b510-4517-bd64-08f2bcc1216e.png)

To check if Apache is working on any browser public ip address of my ec2 instance on port: 80

http://ec2-18-134-155-184.eu-west-2.compute.amazonaws.com/

![image](https://user-images.githubusercontent.com/55473846/138330308-1a405978-f99a-4b82-8d65-2ef91b3093a3.png)

INSTALLED MYSQL

Now that my webserver Apache is working, I will now install the database backend engine MySQl
sudo apt install mysql-server

![image](https://user-images.githubusercontent.com/55473846/138330547-3dc39ce7-bafd-4880-8bda-e7586bcb25f7.png)

To remove some insecure setting issues and to lock down access to the database I ran this command
sudo mysql_secure_installation


![image](https://user-images.githubusercontent.com/55473846/138331309-81cabbd4-390b-4129-a402-bd15466e5fe7.png)

To remove some insecure setting issues and to lock down access to the database I ran this command

sudo mysql_secure_installation

![image](https://user-images.githubusercontent.com/55473846/138331843-d42b2782-3b86-42ed-aac4-fec4233e6b27.png)

To test if can logon to the console I ran the command below

sudo mysql

![image](https://user-images.githubusercontent.com/55473846/138332030-002b061c-1a9e-463f-9fc8-23f8641dfbd9.png)

INSTALLING PHP

The MySQL server is now installed to serve as my database backend and its secured. i already installed Apache to serve my web content, next, I will install PHP to process my code display

I ran the code below

sudo apt install php libapache2-mod-php php-mysql

![image](https://user-images.githubusercontent.com/55473846/138332476-d13b6a31-9df8-4f7d-9600-5c5147db0238.png)

I ran php -v to confirm my php is running

![image](https://user-images.githubusercontent.com/55473846/138332613-73f264f7-08c2-45b9-889f-9fa7d3b46516.png)

I next configure a virtual host for next step
I first created a directory for my project called project Lamp by running the command below

sudo mkdir /var/www/projectlamp

I now assign ownership of the directory to the owner by running the command

sudo chown -R $USER:$USER /var/www/project lamp

I created and opened a new configuration file in Apache’s sites-available directory and inside I have projectlamp.conf

sudo vi /etc/apache2/sites-available/projectlamp.conf

inside the above I inserted the below configuration 

<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

And when I ran 

sudo ls /etc/apache2/sites-available

![image](https://user-images.githubusercontent.com/55473846/138332901-a339d885-5a8d-4cae-8bc4-ad77e47e0b5d.png)

To enable the virtual host, I ran the below command

sudo a2ensite projectlamp

![image](https://user-images.githubusercontent.com/55473846/138333029-1b3fa091-7324-4c4e-86bc-f5ce87beeaeb.png)

Since am not using a Doman site I need to remove Apache default settings and I ran the command below

sudo a2dissite 000-default

![image](https://user-images.githubusercontent.com/55473846/138333251-63df2b19-6fb2-4c10-9f5c-eadc9a3ace88.png)

To make sure no syntax errors I ran the command below

sudo apache2ctl configtest

![image](https://user-images.githubusercontent.com/55473846/138333494-0ba9d8ce-6294-4603-80a8-fefdff5b168f.png)

Finally, to make these changes comes into effect I ran

sudo systemctl reload apache2

Now although the website is ready, but I still need to make website root have some content to serve. web root /var/www/projectlamp is still empty

 Meaning i ran this command to affect that

sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/project lamp/index.html

After running the above command above and click on the public ip address of my ec2 instance

 my webserver Apache now looks like this below
 
ENABLING PHP ON MY WEBSITE

![image](https://user-images.githubusercontent.com/55473846/138333838-4a4dd7bd-7958-4226-a587-f2c85e9c2eae.png)

I changed the website landing page to index .php by running this command to open 
etc/apache2/mods-enabled/dir.conf  the directory

sudo vim /etc/apache2/mods-enabled/dir.conf

and I entered the code below

<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>

Saved and closed the file using vim editor.

![image](https://user-images.githubusercontent.com/55473846/138334223-a0a494e9-94d1-4839-8b4a-11fc5173a2cd.png)

I ran the code below command to load the page again

sudo systemctl reload apache2

 and the page failed to reload with this error shown below

![image](https://user-images.githubusercontent.com/55473846/138334393-7dbbd6d4-d169-4dba-a202-c1a8dd036b84.png)

I resolved the error by running
Sudo apachectl -t
Sudo systemctl status apache2.service
Located the error and removed it
finally ran and created a file called index.php inside this root folder below
vim /var/www/projectlamp/index.php
entered
<?php
phpinfo();
I finally refreshed the webserver page and lunched

![image](https://user-images.githubusercontent.com/55473846/138334739-5519e416-f3ac-4781-a154-e7d8e1c9ed3a.png)

Finally, as the above page contains sensitive information, I ran the below command to remove the sensitive file
sudo rm /var/www/projectlamp/index.php













