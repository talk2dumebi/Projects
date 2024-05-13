#   DEVOPS TOOLING WEBSITE SOLUTION

In this project, we will design and deploy a comprehensive solution using Amazon Web Services (AWS), integrating a range

of vital components to create a cohesive and high-performing system. The key elements of our solution include:

-   Infrastructure: Leveraging the capabilities of AWS to establish a robust and scalable foundation for our project.

-   Webserver Linux: Deploying three instances of Red Hat Enterprise Linux 8 AMI on EC2 to build a reliable and 

    responsive web server environment.

-   Database Server: Setting up a MySQL database server on Ubuntu 20.04 to manage data storage and retrieval efficiently.

-   Storage Server (NFS): Incorporating a dedicated storage server using Red Hat Enterprise Linux 8 and NFS Server 

    technology, enabling seamless file sharing and data accessibility.

-   Programming Language: Utilizing PHP as the primary programming language to develop dynamic and interactive web 

    applications, enhancing user engagement and interactivity.

-   Code Repository: Managing our project's source code efficiently through GitHub, ensuring version control and

    collaboration.

    ####  This project represents a holistic approach to system design, implementation, and management, utilizing AWS and incorporating critical components such as web servers, databases, storage (NFS), and programming, all united to deliver a unified and efficient solution.

    The architecture below shows a common pattern where several stateless Web Servers share a common database and also access the same files using Network File Sytem (NFS) as a shared file storage. Even though the NFS server might be located on a completely separate hardware – for Web Servers it look like a local file system from where they can serve the same files.

    ![alt text](<images_10/Screenshot 2024-04-26 133546.png>)

##  STEP 1 – PREPARE NFS SERVER

-  Spin up a new EC2 instance with RHEL Linux 8 Operating System

![alt text](<images_10/Screenshot 2024-04-26 134611.png>)

-  Configure LVM on the server

![alt text](<images_10/Screenshot 2024-04-26 135053.png>)

-  Format the logical volumes as an xfs filesystem

    `sudo mkfs -t xfs /dev/nfsdata-vg/apps-lv`

    `sudo mkfs -t xfs /dev/nfsdata-vg/logs-lv`

    `sudo mkfs -t xfs /dev/nfsdata-vg/opt-lv`

-  Create 3 Logical Volumes: lv-opt lv-apps, and lv-logs

-  Create mount points on /mnt directory for the logical volumes as follow.

    `sudo mkdir -p /mnt/logs`

    `sudo mkdir -p /mnt/opt`

    `sudo mkdir -p /mnt/apps`

-   Mount lv-apps on /mnt/apps – To be used by webservers

    `sudo mount /dev/nfsdata-vg/logs-lv /mnt/apps`

-   Mount lv-logs on /mnt/logs – To be used by webserver logs

    `sudo mount /dev/nfsdata-vg/opt-lv /mnt/opt`

-   Mount lv-opt on /mnt/opt – To be used by Jenkins server in the next project.

    `sudo mount /dev/nfsdata-vg/logs-lv /mnt/logs`

![alt text](<images_10/Screenshot 2024-04-26 152907.png>)

-   Once mount is completed run sudo blkid to get the UUID of the mount part, open and paste the UUID in the fstab file.

    `sudo vi /etc/fstab`

![alt text](<images_10/Screenshot 2024-04-26 153322.png>)

-   Reload daemon

    `sudo mount -a` 

    `sudo systemctl daemon-reload`

2.  Install the NFS server, configure it to start on reboot, and make sure it is up and running.

    `sudo yum -y update`

    `sudo yum install nfs-utils -y`

    `sudo systemctl start nfs-server.service`

    `sudo systemctl enable nfs-server.service`

    `sudo systemctl status nfs-server.service`

![alt text](<images_10/Screenshot 2024-04-26 155424.png>)

3.  Export the mounts for webservers’ subnet cidr to connect as clients. In this project, we will keep things simple by

    installing all three webservers inside the same subnet, but in production, these will probably be kept in different 
 
    subnets for a higher level of security.

    To check the subnet cidr, open the properties of your EC2 instance on the AWS console and click on the “Network” tab, 
    
    open the “Subnet ID” link in a new tab, and locate “IPv4 CIDR”

![alt text](<images_10/Screenshot 2024-04-26 161138.png>)

-   Set up permissions that will allow our Web servers to read, write, and execute files on NFS.

    `sudo chown -R nobody: /mnt/apps`

    `sudo chown -R nobody: /mnt/logs`

    `sudo chown -R nobody: /mnt/opt`

    `sudo chmod -R 777 /mnt/apps`

    `sudo chmod -R 777 /mnt/logs`

    `sudo chmod -R 777 /mnt/opt`

    `sudo systemctl restart nfs-server.service`

![alt text](<images_10/Screenshot 2024-04-26 162311.png>)

-   Configure access to NFS for clients within the same subnet (example of Subnet CIDR — `Cidr` ):

    `sudo vi /etc/exports`

    `/mnt/apps 172.31.16.0/20(rw,sync,no_all_squash,no_root_squash)`

    `/mnt/logs 172.31.16.0/20(rw,sync,no_all_squash,no_root_squash)`

    `/mnt/opt 172.31.16.0/20(rw,sync,no_all_squash,no_root_squash)`

    
    `sudo exportfs -arv`

 ![alt text](<images_10/Screenshot 2024-04-26 163040.png>)

 4. Check which port is used by NFS and open it using Security Groups. In order for NFS server to be accessible from your
 
    client, you must also open the following ports: TCP 111, UDP 111 in addition to the NFS port.

    `rpcinfo -p | grep nfs`

![alt text](<images_10/Screenshot 2024-04-26 163628.png>)


![alt text](<images_10/Screenshot 2024-04-26 164858.png>)

##  STEP 2 — CONFIGURE THE DATABASE SERVER

-   Configure a MySQL DBMS to work with remote Web Server

-   Install MySQL server

-   Create a database and name it 'tooling'

-   Create a database user and name it 'webaccess'

-   Grant permission to 'webaccess' user on 'tooling' database to do anything only from the webservers subnet

    cidr.

Test if you can access the db-server remotely with this webaccess user.

![alt text](<images_10/Screenshot 2024-04-26 212708.png>)

##  Step 4: Prepare the Web Servers

In this step, we will be launching three web servers. We need to make sure that the web servers can serve the same 

content from shared storage solutions, which in this case are the MySQL database and NFS server.

For storing shared files that our Web Servers will use, we will utilize NFS and mount previously created logical Volume 

`lv-apps` to the folder where Apache stores files to be served to the users `(/var/www)`.

This approach will make our Web Servers `stateless`, which means we will be able to add new ones or remove them whenever

we need, and the integrity of the data (in the database and on NFS) will be preserved.


1.  Launch a new EC2 instance with RHEL 8 Operating System

2.  Install NFS client

    `sudo yum update -y`

    `sudo yum install nfs-utils nfs4-acl-tools -y`

3.  Mount /var/www/ and target the NFS server’s export for apps

    `sudo mkdir /var/www`

    `sudo mount -t nfs -o rw,nosuid 172.31.23.174:/mnt/apps /var/www`

4.  Verify that NFS was mounted successfully by running df -h. Make sure that the changes will persist on the Web Server 

    after reboot by adding the below text to the /etc/fstab file and reload daemon:  

![alt text](<images_10/Screenshot 2024-04-26 224610.png>)

5. Install Remi’s repository, Apache and PHP

    `sudo yum install git -y`

    `sudo yum install httpd -y`

    `sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm -y`

    `sudo dnf install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm -y`

    `sudo dnf module reset php -y -y`

    `sudo dnf module enable php:remi-7.4 -y`

    `sudo dnf install php php-opcache php-gd php-curl php-mysqlnd -y -y`

    `sudo systemctl start php-fpm`

    `sudo systemctl enable php-fpm`

    `sudo setsebool -P httpd_execmem 1`


![alt text](<images_10/Screenshot 2024-04-26 225915.png>)

-   ###   Repeat steps 1–5 for the other 2 Web servers.

6.  Verify that Apache files and directories are available on the Web Server in `/var/www` and also on the NFS server in /

    `mnt/apps`. If you see the same files, it means NFS is mounted correctly. You can test this by creating a new file 
    
    from one web server and check if it is accessible from other web servers.

![alt text](<images_10/Screenshot 2024-04-26 231406.png>)

![alt text](<images_10/Screenshot 2024-04-26 231521.png>)

7.  Locate the log folder for Apache on the Web Server and mount it to NFS server’s export for logs. Repeat step 4 to 

    make sure the mount point will persist after reboot.

    `sudo mount -t nfs -o rw,nosuid 172.31.23.174:/mnt/logs /var/log/httpd`

### Step 5: Deploy a Tooling Application to our Web Server into a Shared NFS Folder

1.  Fork the tooling source code from Darey.io Github Account to your Github account.

2.  Begin by installing git on the webserver: sudo yum install git -y

3.  Initialize Git: git init

![alt text](<../Project_9_Web Solution with Wordpress/images_9/Screenshot 2024-05-12 223432.png>)

4.  Then run: git clone https://github.com/darey-io/tooling.git

![alt text](<../Project_9_Web Solution with Wordpress/images_9/Screenshot 2024-05-12 223533.png>)

5.  Deploy the tooling website’s code to the Webserver. Ensure that the html folder from the repository is deployed to 

`/var/www/html`

![alt text](<../Project_9_Web Solution with Wordpress/images_9/Screenshot 2024-05-12 224131.png>)

6.  On the webserver, ensure port 80 in open to all traffic in the security groups. Attempt to restart httpd service, it very likely that it will fail to start at this point stating that httpd service is unable to write to the log directory. If you encounter this error, check permissions to your /var/www/html folder to ensure that it is own by root.

Note.: Disable SELinux by running `sudo setenforce 0`
To make this change permanent, open following config file `sudo vi /etc/sysconfig/selinux` and set SELINUX=disabled then restart httpd.

7.  Update the website’s configuration to connect to the database: `sudo vi /var/www/html/functions.php`

8.  Apply tooling-db.sql script to your database using this command `mysqli_connect('<Private_IP_DB>', 'webaccess','password', 'tooling')`

![alt text](<../Project_9_Web Solution with Wordpress/images_9/Screenshot 2024-05-12 225442.png>)

9.  In the databse server update the bind address to 0.0.0.0: `sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf`

![alt text](<../Project_9_Web Solution with Wordpress/images_9/Screenshot 2024-05-13 021036.png>)

10. Then create in MySQL a new admin user with username: `myuser` and password: `password`:

![alt text](<../Project_9_Web Solution with Wordpress/images_9/Screenshot 2024-05-13 010537.png>)
    
11. Finally, open the website in your browser with the public IP of the webserver and make sure you can login into the 

    website with myuser user.

![alt text](<../Project_9_Web Solution with Wordpress/images_9/Screenshot 2024-05-13 022019.png>)

![alt text](<../Project_9_Web Solution with Wordpress/images_9/Screenshot 2024-05-13 013556.png>)
    

Thank you...
    
    
    
    
    
    
    
    
   

