#   Step One    Installing Apache and Updating the Firewall

Installing Apache using Ubuntu package manager `apt`

1.  The first thing to do is run the command `sudo apt update` to update to the lastest  package information available for the packages currently installed on the system.

![Alt text](<images_3/Screenshot 2024-01-13 201535.png>)

2.  Next is to run this command to install apache2 `sudo apt install apache2`

![Alt text](<images_3/Screenshot 2024-01-13 203310.png>)

To verify apache2 is install on the OS this command must be run `sudo systemctl status apache2`

![Alt text](<images_3/Screenshot 2024-01-13 204159.png>)

