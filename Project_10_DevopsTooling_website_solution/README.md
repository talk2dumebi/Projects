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

-   Grant permission to 'webaccess' user on 'tooling' database to do anything only from the webservers subnet cidr.