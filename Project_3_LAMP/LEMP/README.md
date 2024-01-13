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


##   Step Two    Installing Msql

