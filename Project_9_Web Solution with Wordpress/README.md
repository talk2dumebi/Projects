#   Understanding 3 Tier Architecture
##  Web Solution with WordPress

-   WordPress is a free and open-source content management system (CMS) written in hypertext preprocessor language[PHP] and paired with a MySQL or MariaDB database with supported HTTPS. 

-   WordPress is a factory that makes webpages: It stores content and enables a user to create and publish webpages, requiring nothing beyond a domain and a hosting service.

-   Generally, web, or mobile solutions are implemented based on what is called the Three-tier Architecture; a client-server software architecture pattern that comprise of 3 separate layers: 

##   Implementing LVM on linux servers (Web and Database servers)

1.  Presentation Layer (PL): This is the user interface such as the client server or browser on your laptop.

2.  Business Layer (BL): This is the backend program that implements business logic. Application or Webserver 

3.  Data Access or Management Layer (DAL): This is the layer for computer data storage and data access. Database Server 

    or File System Server such as FTP server, or NFS Server.

![alt text](image_9/Three-Tier-architecture.png)

In this project, we shall:

-   Configure storage subsystem for Web and Database servers based on Linux OS. This part focuses on practical experience of working with disks, partitions and volumes in Linux.

-   Install WordPress and connect it to a remote MySQL database server. This part will soldify our skills of deploying Web and DB tiers of Web solution.

##  Step 1 — Prepare a Web Server

1.   Launch an EC2 instance that will serve as "Web Server". Create 3 EBS volumes in the same AZ as your Web Server EC2,

    each of 10 GiB size.

2.   Attach each of the EBS volumes to your web server instance.

![alt text](<image_9/Screenshot 2024-04-17 010557.png>)

3.   Open up the Linux terminal to begin configuration, ssh into your server.

4.   Use `lsblk` command to inspect what block devices are attached to the server. All devices in Linux reside in /dev/
 
    directory. Inspect it with ls /dev/ and make sure you see all 3 newly created block devices there; their names will 
 
    likely be xvdf, xvdh, xvdg.

![alt text](<image_9/Screenshot 2024-04-17 012343.png>)

5.  Use `df -h` command to see all mounts and free space on the server.

![alt text](<image_9/Screenshot 2024-04-17 013628.png>)

6.  Use gdisk utility to create a single partition (10GB) on each of the 3 disks:

`sudo gdisk /dev/xvdf`
`sudo gdisk /dev/xvdg`
`sudo gdisk /dev/xvdh`

![alt text](<image_9/Screenshot 2024-04-17 032527.png>)

7.  Use `lsblk` utility to view the newly configured partition on each of the 3 disks.

![alt text](<image_9/Screenshot 2024-04-17 032226.png>)

8.  Install `lvm2` package using `sudo yum install lvm2`. Run `sudo lvmdiskscan` command to check for available 

    partitions.

![alt text](<image_9/Screenshot 2024-04-17 033217.png>)

9.  Use `pvcreate` utility to mark each of 3 disks as physical volumes (PVs) to be used by LVM.

`sudo pvcreate /dev/xvdf1 pvcreate /dev/xvdg1 pvcreate /dev/xvdh1`

![alt text](<image_9/Screenshot 2024-04-17 034305.png>)

10. Verify that the physical volumes were created successfully by running `sudo pvs`.

![alt text](<image_9/Screenshot 2024-04-17 034005.png>)

11. Using the `vgcreate` utility, create a volume group named `webdata-vg` and add all the three PVS to the volume group.

`sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1`

![alt text](<image_9/Screenshot 2024-04-17 035014.png>)

12. Verify that the volume group was created successfully using `sudo vgs`

![alt text](<image_9/Screenshot 2024-04-17 035235.png>)

13. Using the `lvcreate`  utility, create two logical volumes(LVs); `apps-lv` and `logs-lv`. Assign each LVs about half

 of the volume group size which is about 30GB. I assigned both 14GB size; apps-lv will be used to store data for the 

 Website while logs-lv will be used to store data for logs. Using this command below.

 `sudo lvcreate -n apps-lv -L 14G webdata-vg`

`sudo lvcreate -n logs-lv -L 14G webdata-vg`

![alt text](<image_9/Screenshot 2024-04-17 040419.png>)

14. Verify that the LVs were created successfully using `sudo lvs`.

![alt text](<image_9/Screenshot 2024-04-17 040632.png>)

15. Verify the entire setup. Using this command.

`sudo vgdisplay -v #view complete setup - VG, PV, and LV`

`sudo lsblk`

![alt text](<image_9/Screenshot 2024-04-17 041246.png>)

16. Use `mkfs.ext4` to format the logical volumes with `ext4 filesystem`. Using the following command.

`sudo mkfs -t ext4 /dev/webdata-vg/apps-lv`

![alt text](<image_9/Screenshot 2024-04-18 215057.png>)

`sudo mkfs -t ext4 /dev/webdata-vg/logs-lv`

![alt text](<image_9/Screenshot 2024-04-18 215209.png>)

17. Create /var/www/html directory to store website files.

`sudo mkdir -p /var/www/html`

18. Create /home/recovery/logs to store backup of log data:

`sudo mkdir -p /home/recovery/logs`

19. Mount /var/www/html on apps-lv logical volume:

`sudo mount /dev/webdata-vg/apps-lv /var/www/html/`

We shall mount 'logs-lv' logical volume on /var/log directory . Since this mount point isn't an empty directory, there is need to backup its content before mounting as mounting would cover up this content and will render it unavailable until one unmounts.

20. Use `rsync` utility to backup all the files in the log directory /var/log into /home/recovery/logs.

`sudo rsync -av /var/log/. /home/recovery/logs/`

21. Proceed to mount logs-lv logical volume on /var/log. (Note that all the existing data on /var/log will be covered 

up and rendered unavailable to whatever process uses them).

`sudo mount /dev/webdata-vg/logs-lv /var/log`

22. Then, we restore the log files back into /var/log directory.

`sudo rsync -av /home/recovery/logs/. /var/log`

TIP:

-   Rsync is a free software utility for Unix- and Linux-like systems that copies files and directories from one host to 

    another. 

-   It is considered to be a lightweight application because file transfers are incremental.

-   After the initial full transfer, only bits in files that have been changed are transferred.

23. Update the `/etc/fstab` file to make persistent the mount configuration even after a system reboot.

-   The UUID of the device will be used to update the `/etc/fstab` file.

` sudo blkid`

![alt text](<image_9/Screenshot 2024-04-18 222259.png>)

` sudo vi /etc/fstab`

![alt text](<image_9/Screenshot 2024-04-18 224013.png>)

24. Test the configuration and reload the daemon.  `sudo mount -a`  `sudo systemctl daemon-reload`

25. Verify the setup by running `df -h`

![alt text](<image_9/Screenshot 2024-04-18 224613.png>)


##   Installing wordpress and configuring to use MYSQL Database

###  Step 2 — Prepare the Database Server

-   A second RedHat EC2 instance was launched and the above steps were repeated. instead of `apps-lv` logical volume,

    `db-lv` was created and mounted to `/db` directory instead of `/var/www/html` directory.

### Step 3 — Install WordPress on the Web Server EC2

1.  Updating the server 

    `sudo yum update -y`

2. Install wget, Apache and it's dependencies

    `sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json`

3. Start Apache

    `sudo systemctl enable httpd`

    `sudo systemctl start httpd`

4.  To install PHP and it's dependencies

    `sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`

    `sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm`

    `sudo yum module list php`

    `sudo yum module reset php`

    `sudo yum module enable php:remi-7.4`

    `sudo yum install php php-opcache php-gd php-curl php-mysqlnd`

    `sudo systemctl start php-fpm`

    `sudo systemctl enable php-fpm`

    `setsebool -P httpd_execmem 1`

5.  Restart Apache

    `sudo systemctl restart httpd`

6.  Download wordpress and copy wordpress to `var/www/html`

    `mkdir wordpress`

    `cd  wordpress`

    `sudo wget http://wordpress.org/latest.tar.gz`

    `sudo tar xzvf latest.tar.gz`

    `sudo rm -rf latest.tar.gz`

    `cp wordpress/wp-config-sample.php wordpress/wp-config.php`

    `cp -R wordpress/. /var/www/html/`

7.  Configure SELinux Policies

    `sudo chown -R apache:apache /var/www/html/wordpress`

    `sudo chcon -t httpd_sys_rw_content_t /var/www/html/wordpress -R`

    `sudo setsebool -P httpd_can_network_connect=1`

###  Step 4 — Install MySQL on your DB Server EC2

1.  Update and install mysql server:

    `sudo yum update`

    `sudo yum install mysql-server`

2.  Verify that the service is up and running by using `sudo systemctl status` mysqld`. If the service is not running 

    restart and enable with this command.

    `sudo systemctl restart mysqld`

    `sudo systemctl enable mysqld`

###  Step 5 — Configure DB to work with WordPress

    sudo mysql

    CREATE DATABASE wordpress;

    CREATE USER 'myuser'@'<insert private IP>' IDENTIFIED BY 'mypass'; 

    GRANT ALL ON wordpress.* TO 'myuser'@'172.31.92.2';

    FLUSH PRIVILEGES;

    SHOW DATABASES;

    exit

### Step 6 — Configure WordPress to connect to remote database.

Hint: Do not forget to open MySQL port 3306 on DB Server EC2. For extra security, you shall allow access to the DB server

ONLY from your Web Server’s IP address, so in the Inbound Rule configuration specify source as /32.

![alt text](<image_9/Screenshot 2024-04-21 142033.png>)

1. Install MySQL client and test that you can connect from your Web Server to your DB server by using mysql-client

    `sudo yum install mysql`

    `sudo mysql -u myuser -p -h <>`

2.  Verify if you can successfully execute SHOW DATABASES; command and see a list of existing databases.

3.  Change permissions and configuration so Apache could use WordPress.

4.  Enable TCP port 80 in Inbound Rules configuration for your Web Server EC2 (enable from everywhere 0.0.0.0/0 or from 

    your workstation’s IP).

5.  Try to access from your browser the link to your WordPresshttp://<Webserver-Publiuc-IP>/wordpress/

![alt text](<image_9/Screenshot 2024-04-21 143051.png>)

    Click Let’go, complete the login details and hit continue

![alt text](<image_9/Screenshot 2024-04-21 143457.png>)

If you see this message — it means WordPress has successfully connected to your remote MySQL database.

![alt text](<image_9/Screenshot 2024-04-21 143637.png>)

Thank you...


