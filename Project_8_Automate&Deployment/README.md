#   Automating Loadbalancer configuration with Shell Scripting

##  Automate the Deployment of Webservers

In the implementing load balancer with Nginx course. We deployed two backend servers, with a load balancer distributing traffic across the webservers. We did that by typing command right on our terminal.

###  Deploying and Configuring the Webservers

Following the steps below to run the script:

1. Provision an EC2 instance running Ubuntu. 

![alt text](<images_8/Screenshot 2024-03-24 190425.png>)

2. Open port 8000 to allow traffic from anywhere using the security group.

![alt text](<images_8/Screenshot 2024-03-24 192637.png>)

3. Connect to the webserver via the terminal using SSH client

![alt text](<images_8/Screenshot 2024-03-24 193322.png>)

4. Open a file using this command `sudo vi install.sh` and paste the script.

![alt text](<images_8/Screenshot 2024-03-24 202902.png>)

5. Change the permission on the file to make an executable using this command `sudo chmod +x install.sh`

![alt text](<images_8/Screenshot 2024-03-24 203623.png>)

6. Run the shell script using this command `./install.sh`

![alt text](<images_8/Screenshot 2024-03-24 204454.png>)

#   Deployment of Nginx as a Load Balancer using Shell script

##   Deployment of Nginx as a Load Balancer using Shell script

Having successfully deployed and configured two webservers. We need to moved on to the load balancer, and provision an EC2 instance running ubuntu, open port 80 to anywhere using the security group and connect to the load balance via the terminal.

### Deploying and Configuring Nginx Load Balancer

####    Steps to Run the Shell Script

1. On the terminal open a file nginx.sh using this command 

`sudo vi nginx.sh`

2. Copy and paste the script inside the file.

![alt text](<images_8/Screenshot 2024-03-24 212320.png>)

3. Close the file using this command 

`type esc the shift + :wqa!`

4. Change the file permission to make it an executable using this command `sudo chmod +x nginx.sh`

![alt text](<images_8/Screenshot 2024-03-24 212424.png>)

5. Run the script with this command `./nginx.sh`

![alt text](<images_8/Screenshot 2024-03-24 214722.png>)

##  Verifying the setup

Screenshot for web001_server

![alt text](<images_8/Screenshot 2024-03-24 215153.png>)

Screenshot for web001_server

![alt text](<images_8/Screenshot 2024-03-24 215208.png>)


Thank you...