#   Implementing LoadBalancers with Nginx

##  Understanding to Load Balancing and Nginx

Load balancing prevents a website from becoming crippled when there’s an overflow of requests. A load balancer sends requests to servers that can efficiently handle them to maximize speed and performance.

###   Setting Up a basic Load Balancer

###   Step One: Provisioning EC2 instance

. Open the AWS Management Console, click on EC2. Scroll down the page and click on launch instance.

![alt text](<images_7/Screenshot 2024-03-08 215644.png>)

![alt text](<images_7/Screenshot 2024-03-08 215919.png>)

. Under Name, Provide a unique name for each of the webservers you want launch.

![alt text](<images_7/Screenshot 2024-03-08 220356.png>)

. Under Applications and OS images, click on quick start and click on ubuntu

![alt text](<images_7/Screenshot 2024-03-08 220728.png>)

. Under Key Pair, click on create new key pair if you do not have one. You can use the same key pair for all the instances you provision.

![alt text](<images_7/Screenshot 2024-03-08 231432.png>)

. And Finally click on launch instance.

![alt text](<images_7/Screenshot 2024-03-08 231723.png>)

###   Step Two: 

. Open port 8000. We will be running the webservers on port 8000 while the load balancers runs on port 80. We need to open the 8000 to allow traffic from anywhere. 

. Click on the instance ID to get details of the EC2 instance.

![alt text](<images_7/Screenshot 2024-03-08 233124.png>)

. On that same page, scroll down and click on security.

![alt text](<images_7/Screenshot 2024-03-08 233639.png>)

. Click on security group.

![alt text](<images_7/Screenshot 2024-03-08 233923.png>)

. On the top of the page click on Action and select Edit inbound rules.

![alt text](<images_7/Screenshot 2024-03-08 234408.png>)

. Add the rules.

![alt text](<images_7/Screenshot 2024-03-08 234733.png>)

. Click on save rules.

![alt text](<images_7/Screenshot 2024-03-08 235158.png>)

###   Step Three: Install Apache Webserver

After provisioning both of the servers and have opened the necessary ports. Its time to install apache software on both servers. To do so we must first connect to the webserver via ssh. Then we can now run commands on the terminal the webservers.

. Connecting to the webserver: To connect to the webserver, click on the instance ID, at the top of the page click on connect.

![alt text](<images_7/Screenshot 2024-03-09 002027.png>)

. Next copy the ssh command below:

![alt text](<images_7/Screenshot 2024-03-09 003603.png>)

. Open a terminal (your prefer terminal) in our local machine, paste the ssh and follow the step.

![alt text](<images_7/Screenshot 2024-03-09 003647.png>)

. After the steps giving we should be connected to a terminal on the instance.

![alt text](<images_7/Screenshot 2024-03-09 004702.png>)

. Next install apache with this command:

`sudo apt update -y &&  sudo apt install apache2 -y`

![alt text](<images_7/Screenshot 2024-03-09 010026.png>)

. Verify if Apache is running using this command:

`sudo systemctl status apache2`

![alt text](<images_7/Screenshot 2024-03-09 010301.png>)

