#   #   LAMP STACK implementation

##   Step One    Installing the Nginx Web Server

1.  The first thing to do is run the command `sudo apt update` to update to the lastest  package information available for the packages currently installed on the system.

![Alt text](<images_4/Screenshot 2024-01-19 232452.png>)

2.  Next is to run this command to install apache2 `sudo apt install nginx`

![Alt text](<images_4/Screenshot 2024-01-19 232826.png>)

3.  To verify nginx is install and runing as a service on Ubuntu this command must be run `sudo systemctl status nginx`

![Alt text](<images_4/Screenshot 2024-01-20 002809.png>)

4.  After checking the installation of nginx, the next is to check if nginx is responding to the internet. `http://<Public-IP-Address>:80`

![Alt text](<images_4/Screenshot 2024-01-20 003121.png>)


#   Installing Mysql

##  Step Two: installing MySQL

Now that the web server is up and running, it is time to install MySQL. MySQL is a database management system. Basically, it will organize and provide access to databases where the site can store information. To install
MYSQL run this command `sudo apt install mysql-server`

![Alt text](<images_4/Screenshot 2024-01-20 003627.png>)

After installation log into MYSQL console with this command `sudo mysql`

![Alt text](<images_4/Screenshot 2024-01-20 004018.png>)

Next, this command `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';` is run to set password for the root user.

![Alt text](<images_4/Screenshot 2024-01-20 004501.png>)

