#   Understanding 3 Tier Architecture
##  Web Solution with WordPress

-   WordPress is a free and open-source content management system (CMS) written in hypertext preprocessor language[PHP] and paired with a MySQL or MariaDB database with supported HTTPS. 

-   WordPress is a factory that makes webpages: It stores content and enables a user to create and publish webpages, requiring nothing beyond a domain and a hosting service.

-   Generally, web, or mobile solutions are implemented based on what is called the Three-tier Architecture; a client-server software architecture pattern that comprise of 3 separate layers: 

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

`sudo pvcreate /dev/xvdf1`

`sudo pvcreate /dev/xvdg1`

`sudo pvcreate /dev/xvdh1`




