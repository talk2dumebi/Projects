#   #   LEMP STACK implementation

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

Then we exist Mysql using this command `exit`

![Alt text](<images_4/Screenshot 2024-01-20 004818.png>)

When the installation is complete, run a simple security script that comes pre-installed with MySQL which will remove some dangerous defaults and lock down access to your database system. Start the interactive script by running. `sudo mysql_secure_installation`

![Alt text](<images_4/Screenshot 2024-01-20 005356.png>)

This will ask if you want to configure the VALIDATE PASSWORD PLUGIN.

![Alt text](<images_4/Screenshot 2024-01-20 005822.png>)

If you answer “yes”, you’ll be asked to select a level of password validation. Keep in mind that if you enter 2 for the strongest level, you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters, or which is based on common dictionary words.

![Alt text](<images_4/Screenshot 2024-01-20 010040.png>)

Regardless of whether you chose to set up the VALIDATE PASSWORD PLUGIN, your server will next ask you to select and confirm a password for the MySQL root user. This is not to be confused with the system root. The database root user is an administrative user with full privileges over the database system. Even though the default authentication method for the MySQL root user dispenses the use of a password, even when one is set, you should define a strong password here as an additional safety measure. We’ll talk about this in a moment.

If you’ve enabled password validation, you’ll be shown the password strength for the root password you just entered and your server will ask if you want to change that password. If you are happy with your current password, enter N for “no” at the prompt.

![Alt text](<images_4/Screenshot 2024-01-20 010707.png>)

When you’re finished, test if you’re able to log in to the MySQL console by typing.

![Alt text](<images_4/Screenshot 2024-01-20 010935.png>)

To exist from MYSQL console `exit`

![Alt text](<images_4/Screenshot 2024-01-20 011118.png>)



#   Enable PHP on the website

##  Step Three:  Enable PHP on the website

You have Nginx installed to serve your content and MySQL installed to store and manage your data. Now you can install PHP to process code and generate dynamic content for the web server.

While Apache embeds the PHP interpreter in each request, Nginx requires an external program to handle PHP processing and act as a bridge between the PHP interpreter itself and the web server.

To install php we need to install `php8.1-fpm` and `php-mysql`.

![Alt text](<images_4/Screenshot 2024-01-20 012051.png>)


#   Step Four   Configuring Nginx to Use the PHP Processor

##   Configuring Nginx to Use the PHP Processor

When using the Nginx web server, we can create server blocks (similar to virtual hosts in Apache) to encapsulate configuration details and host more than one domain on a single server. In this guide, we’ll use projectLEMP as an example domain name.

Create the root web directory for your_domain(projectLEMP) `sudo mkdir /var/www/projectLEMP`

![Alt text](<images_4/Screenshot 2024-01-20 013203.png>)

Next, we need to assign ownership of the directory with the `$USER` environment variable, which will reference the current system user.

![Alt text](<images_4/Screenshot 2024-01-20 014110.png>)

We then, open a new configuration file in Nginx’s sites-available directory using a preferred command-line edito(nano). `sudo nano /etc/nginx/sites-available/projectLEMP`

![Alt text](<images_4/Screenshot 2024-01-20 015412.png>)

We also need to activate the configuration by linking to the configuration file from Nginx’s sites-enabled directory run this command `sudo ln -s /etc/nginx/sites-available/your_domain /etc/nginx/sites-enabled/`

![Alt text](<images_4/Screenshot 2024-01-20 020454.png>)

Then, unlink the default configuration file from the /sites-enabled/ directory:

![Alt text](<images_4/Screenshot 2024-01-20 020010.png>)

This will tell Nginx to use the configuration next time it is reloaded. You can test your configuration for syntax errors by running the following.

![Alt text](<images_4/Screenshot 2024-01-20 024534.png>)

When ready, reload Nginx to apply the changes.

![Alt text](<images_4/Screenshot 2024-01-20 025419.png>)

The new website is now active, but the web root `/var/www/projectLEMP` is still empty. Create an index.html file in that location so that we can test the new server block works as expected. this command will be run `nano /var/www/projectLEMP/index.html`

![Alt text](<images_4/Screenshot 2024-01-20 030048.png>)

Now we go to the browser and access the server’s domain name or IP address, as listed within the server_name directive in the server block configuration file. To see this...

![Alt text](<images_4/Screenshot 2024-01-20 030625.png>)

If this page shown, it means the Nginx server block is working as expected.


#   Step Five   Testing PHP with Nginx

##  Testing PHP with Nginx


The LEMP stack should now be completely set up. We can test it to validate that Nginx can correctly hand `.php` files off to your PHP processor.

We can do this by creating a test PHP file in your document root. Open a new file called `info.php` within the document root in your preferred text editor. Runing this command `nano /var/www/your_domain/info.php`

![Alt text](<images_4/Screenshot 2024-01-20 031810.png>)

We can now access this page in the web browser by visiting the domain name or public IP address set up in the Nginx configuration file, followed by `/info.php`.

![Alt text](<images_4/Screenshot 2024-01-20 032145.png>)

After checking the relevant information about your PHP server through that page, it’s best to remove the file we created as it contains sensitive information about the PHP environment and the Ubuntu server. We can use `rm` to remove that file. Runing this commands `sudo rm /var/www/your_domain/info.php`

![Alt text](<images_4/Screenshot 2024-01-20 032549.png>)


#   Retrieving Data from MYQSL Database with PHP

##  Retrieving Data from MYQSL Database with PHP

First, connect to the MySQL console using the root account. Runing this commands `mysql -u root -p`

![Alt text](<images_4/Screenshot 2024-01-20 034218.png>)

To create a new database, run the following command from your MySQL console. Runing this commands `CREATE DATABASE example_database;`

![Alt text](<images_4/Screenshot 2024-01-20 034732.png>)

Now you can create a new user and grant them full privileges on the custom database you’ve created.

The following command creates a new user named `example_user`, using `mysql_native_password` as the default authentication method. We’re defining this user’s password as `password`, but you should replace this value with a secure password of your own choosing.

![Alt text](<images_4/Screenshot 2024-01-20 034949.png>)

Now we need to give this user permission over the example_database database:

![Alt text](<images_4/Screenshot 2024-01-20 035203.png>)

This will give the example_user user full privileges over the example_database database while preventing this user from creating or modifying other databases on your server.

Now exit the MySQL shell with the following command.

![Alt text](<images_4/Screenshot 2024-01-20 035432.png>)

You can test if the new user has the proper permissions by logging in to the MySQL console again, this time using the custom user credentials. Notice the -p flag in this command, which will prompt you for the password used when creating the example_user user.

![Alt text](<images_4/Screenshot 2024-01-20 035702.png>)

After logging in to the MySQL console, confirm that you have access to the example_database database.


This will return the following output

![Alt text](<images_4/Screenshot 2024-01-20 035845.png>)

Next, we’ll create a test table named todo_list. From the MySQL console, run the following statement:

![Alt text](<images_4/Screenshot 2024-01-20 040310.png>)

Insert a few rows of content in the test table. You might want to repeat the next command a few times, using different values.

![Alt text](<images_4/Screenshot 2024-01-20 040710.png>)

After confirming that you have valid data in your test table, you can exit the MySQL console:

![Alt text](<images_4/Screenshot 2024-01-20 040908.png>)

Now you can create the PHP script that will connect to MySQL and query for your content. Create a new PHP file in your custom web root directory using your preferred editor. We’ll use nano for that. `nano /var/www/projectLEMP/todo_list.php`

The following PHP script connects to the MySQL database and queries for the content of the todo_list table, exhibiting the results in a list. If there’s a problem with the database connection, it will throw an exception.

Add the following content to your todo_list.php script.

![Alt text](<images_4/Screenshot 2024-01-20 041418.png>)

Save and close the file when you’re done editing.

We can now access this page in the web browser by visiting the domain name or public IP address configured for the website, followed by `/todo_list.php`. We should receive a page like the following

![Alt text](<images_4/Screenshot 2024-01-20 041751.png>)

That means the PHP environment is ready to connect and interact with the MySQL server.


Thank you...






















