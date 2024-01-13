#   LAMP STACK implementation

##   Step One    Installing Apache and Updating the Firewall

Installing Apache using Ubuntu package manager `apt`

1.  The first thing to do is run the command `sudo apt update` to update to the lastest  package information available for the packages currently installed on the system.

![Alt text](<images_3/Screenshot 2024-01-13 201535.png>)

2.  Next is to run this command to install apache2 `sudo apt install apache2`

![Alt text](<images_3/Screenshot 2024-01-13 203310.png>)

3.  To verify apache2 is install on the OS this command must be run `sudo systemctl status apache2`

![Alt text](<images_3/Screenshot 2024-01-13 204159.png>)

4.  After checking the installation of the apache2, the next is to check the Apahe HTTP server responding to the internet. `http://<Public-IP-Address>:80`

![Alt text](<images_3/Screenshot 2024-01-13 204536.png>)


#   Installing Mysql

##  Step Two: installing MySQL

Now that the web server is up and running, it is time to install MySQL. MySQL is a database management system. Basically, it will organize and provide access to databases where the site can store information. To install
MYSQL run this command `sudo apt install mysql-server`

![Alt text](<images_3/Screenshot 2024-01-13 211843.png>)

After installation log into MYSQL console with this command `sudo mysql`

![Alt text](<images_3/Screenshot 2024-01-13 214504.png>)

Next, this command `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';` is run to set password for the root user.

![Alt text](<images_3/Screenshot 2024-01-13 215927.png>)

Then we exist Mysql using this command `exit`

![Alt text](<images_3/Screenshot 2024-01-13 220118.png>)

When the installation is complete, run a simple security script that comes pre-installed with MySQL which will remove some dangerous defaults and lock down access to your database system. Start the interactive script by running. `sudo mysql_secure_installation`

![Alt text](<images_3/Screenshot 2024-01-13 223808.png>)

This will ask if you want to configure the VALIDATE PASSWORD PLUGIN.
![Alt text](<images_3/Screenshot 2024-01-13 223713.png>)

If you answer “yes”, you’ll be asked to select a level of password validation. Keep in mind that if you enter 2 for the strongest level, you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters, or which is based on common dictionary words.

![Alt text](<images_3/Screenshot 2024-01-13 224826.png>)

Regardless of whether you chose to set up the VALIDATE PASSWORD PLUGIN, your server will next ask you to select and confirm a password for the MySQL root user. This is not to be confused with the system root. The database root user is an administrative user with full privileges over the database system. Even though the default authentication method for the MySQL root user dispenses the use of a password, even when one is set, you should define a strong password here as an additional safety measure. We’ll talk about this in a moment.

If you’ve enabled password validation, you’ll be shown the password strength for the root password you just entered and your server will ask if you want to change that password. If you are happy with your current password, enter N for “no” at the prompt.

![Alt text](<images_3/Screenshot 2024-01-13 225105.png>)

When you’re finished, test if you’re able to log in to the MySQL console by typing.

![Alt text](<images_3/Screenshot 2024-01-13 230423.png>)

To exist from MYSQL console `exit`

![Alt text](<images_3/Screenshot 2024-01-13 220118.png>)


#   Installing PHP

##  Step Three:  Installing PHP

PHP is the component of your setup that will process code to display dynamic content. It can run scripts, connect to your MySQL databases to get information, and hand the processed content over to your web server so that it can display the results to your visitors. 

When installing PHP this commands is run `$ sudo apt install php libapache2-mod-php php-mysql`

![Alt text](<images_3/Screenshot 2024-01-13 232201.png>)

To check the PHP version run this command `php -v`
![Alt text](<images_3/Screenshot 2024-01-13 232706.png>)

