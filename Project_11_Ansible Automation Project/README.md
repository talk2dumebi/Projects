#   Ansible Automation Project

##  Ansible Client as a Jump Server (Bastion Host)

A [Jump Server](https://en.wikipedia.org/wiki/Jump_server) sometimes also referred to as [Bastion Host](https://en.wikipedia.org/wiki/Bastion_host) is an intermediary server through which access to the internal network can be provided. If you think about the current architecture you are working on, ideally the Web Servers would be inside a secured network that cannot be reached directly from the Internet. That means DevOps engineers cannot SSH into the Web Servers directly and can only access it through a Jump Server. It provides better security and reduces [attack surface](https://en.wikipedia.org/wiki/Attack_surface).

In the diagram below, the Virtual Private Network (VPC) is divided into two subnets (i.e. Public Subnet has Public IP Addresses and Private Subnet is only reachable by Private IP addresses).


![alt text](<images_11/Screenshot 2024-05-23 024236.png>)