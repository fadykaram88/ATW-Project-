# ATW-Project-
#LAMP PROJECT 

to setup a basic LAMP stack on linux server 

1 install apache 
sudo apt-get install apache2

2 install mySQL
sudo apt-get install mysql-server

3 install PHP 
sudo apt-get install php php-mysql

4 testing PHP 
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php

5 open google and write localhost

6 ensure that apache and mySQL and PHP are active 
sudo systemctl status apache2
sudo systemctl status mysql
php -v 

7 MySQL security
sudo mysql_secure_installation

8 creating new mySQL DB and new user 
sudo mysql
CREATE DATABASE my_database;
CREATE USER 'db_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON my_database.* TO 'db_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;

9 delete PHP file 
sudo rm /var/www/html/info.php

10 install phpmyadmin from google  
https://www.phpmyadmin.net/

11 extract it then put the directort in /var/www/html/fady

12 change the name of the dir to be phpmyadmin

13 change the permission of the folder so Apache can see it 
sudo chmod 400 /var/www/html/fady/phpmyadmin

14 change the port of the apache from 80 becuase jenkins works in port 80 
sudo nano /etc/apache2/ports.conf
Listen 8000
then write 
sudo nano /etc/apache2/sites-enabled/000-default.conf
and modify the text to be <VirtualHost *:8000>

15 restart apache 
sudo systemctl restart apache2

16 open it in google 
http://localhost:8000/phpmyadmin/

17 put the website in AWS instance to make it public to anyone 

A open AWS console 
B create security grouop and in inbound roles choose 
HTTPS with TCP 443 and the source is 0.0.0.0/0
HTTP with  TCP 80  and the source is 0.0.0.0/0
SSH  with  TCP 22  and the source is 0.0.0.0/0

C Create Key pair then download it to a path which is /home/fady/AWS KEY


D launch new EC2 instance 
 choose OS ubuntu  then choose the key pair name then attach it to existing security group 

E go to the directory and open the permission (chmod 400) then open the terminal and write ssh -i /home/fady/'AWS KEY'/baba.pem ubuntu@35.173.188.180

now I am inside the instance 

F sftp -i /home/fady/'AWS KEY'/baba.pem ubuntu@35.173.188.180

G copy the files from my machine into the instance 
put -r phpmyadmin

NOW it is public and now you can open it in google 
http://35.173.188.180/phpmyadmin/


18 upload this project to github 

A git init 
B touch .gitignore
C  git remote add origin https://github.com/fadykaram88/ATW-project.git
D git add .
E git commit -m "Initial commit for ATW project"
F git push -u origin main
https://github.com/fadykaram88/ATW-Project-.git

NETWORK BASICS 

1 IP Address :Internet Protocol addresses and routes packets of data sent between networked devices 

2 MAC Address: (Media Access Control Address) is a unique hardware identifier assigned to a device's network interface card (NIC) by the manufacturer. It ensures devices within the same local network can communicate with each other. Unlike an IP address, which can change, the MAC address is permanent and operates at the data link layer of the OSI model.


3 IP VS MAC : 

MAC address 	                     IP address
48 bit address 	                  32 bit address 
works at OSI layer 2            works at OSI layer 3  
link layer                        network layer 
physical layer                   logical address 
Fixed assigned by             can change depending on  
manufacturer                 the network environment 
00:0C:F5:09:56:E8                 150.60.122.98


4 SWITCHES : connects devices within the same network and uses MAC address to forward data to the correct destination 
EX . Ethernet switch in an office network 

5 ROUTERS : connects multiple networks and directs data packets between them 
EX . Home router connecting a local network to the internet 

6 ROUTING PROTOCOLS :are rules that enable routers to communicate and determine the best paths for data to travel across a network. Their primary roles include:
Path Selection: Choosing the optimal route for data packets based on metrics like hop count or latency.
Network Discovery: Identifying available devices and connections within the network.
Dynamic Updates: Adjusting routes automatically in response to changes such as failures or congestion.
