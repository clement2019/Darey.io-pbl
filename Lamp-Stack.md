### PROJECT 1 WEB STACK IMPLEMENTATION   (LAMP STACK) IN AWS
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




