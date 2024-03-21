# Jump Hosting with NAT in AWS
This repository contains resources and configurations for setting up jump hosting with Network Address Translation (NAT) in AWS. Jump hosting, also known as a jump box or bastion host, is a secure gateway server that allows access to private instances within a Virtual Private Cloud (VPC) from an external network, such as the internet. NAT is used to enable private instances to initiate outbound traffic to the internet through the bastion host.

### Overview
Jump hosting with NAT combines the security benefits of a bastion host with the ability for private instances to access the internet for software updates, package installations, and other outbound communication.

### Components
1. Bastion Host
The bastion host serves as the entry point for accessing private instances within the VPC. It resides in a public subnet and acts as a secure gateway, controlling access to private resources.

2. Private Instances
Private instances are servers or resources that are not directly accessible from the internet. They reside in private subnets within the VPC and rely on the bastion host for inbound and outbound traffic.

3. NAT Gateway
The NAT gateway allows private instances in the VPC to initiate outbound traffic to the internet while keeping them protected from direct inbound access. It provides source network address translation for instances in private subnets.

### Steps to Set Up Jump Hosting with NAT
- ### 1. Create a VPC
- Navigate to the VPC dashboard in the AWS Management Console.
- Click on "Create VPC" and follow the prompts to create a new VPC.
- ![AWS Logo](https://github.com/NimishRathi/Jump-Hosting-AWS/blob/main/Screenshot%202024-03-20%20153625.png)

- ### 2. Create Subnets
- Within your VPC, create at least two subnets: one public and one private.
- Public subnets will have a route to the internet via an Internet Gateway (IGW).
- Private subnets will not have a route to the internet directly.
- ![AWS Logo](https://github.com/NimishRathi/Jump-Hosting-AWS/blob/main/Screenshot%202024-03-20%20154051.png)
- ![AWS Logo](https://github.com/NimishRathi/Jump-Hosting-AWS/blob/main/Screenshot%202024-03-20%20154116.png)

- ### 3. Launch Instances
- Launch EC2 instances in both the public and private subnets.
- The public instance will act as the jump host, and the private instance will host the internal resources.
- Ensure that the security groups allow SSH (or your preferred protocol) access to the jump host from your IP address.
- ![AWS Logo](https://github.com/NimishRathi/Jump-Hosting-AWS/blob/main/Screenshot%202024-03-20%20155648.png)

- ### 4. Configure NAT Gateway
- Navigate to the NAT Gateways section in the VPC dashboard.
- Create a new NAT Gateway in one of the public subnets.
- Update the route tables of your private subnets to route traffic destined for the internet (`0.0.0.0/0`) to the NAT Gateway.
- ![AWS Logo](https://github.com/NimishRathi/Jump-Hosting-AWS/blob/main/Screenshot%202024-03-20%20154229.png)

- ### 5. Update Route Tables
- In the route table for the private subnet, add a route to direct traffic destined for the internet (`0.0.0.0/0`) to the NAT Gateway.
- ![AWS Logo](https://github.com/NimishRathi/Jump-Hosting-AWS/blob/main/Screenshot%202024-03-20%20154103.png)

- ### 6. Test Connectivity
- SSH into the jump host from your local machine using its public IP.
- From the jump host, SSH into the private instance using its private IP.
- Confirm that you can access resources within the private subnet from the jump host.

- ping google.com from bastion host ! alright its working  
![AWS Logo](https://github.com/NimishRathi/Jump-Hosting-AWS/blob/main/Screenshot%202024-03-21%20164823.png)
now ssh into the private instance and try to ping 
![AWS Logo](https://github.com/NimishRathi/Jump-Hosting-AWS/blob/main/Screenshot%202024-03-21%20164850.png)
![AWS Logo](https://github.com/NimishRathi/Jump-Hosting-AWS/blob/main/Screenshot%202024-03-21%20165247.png) 
 Confirm that you can access resources within the private subnet from the jump host.and ping google.com from private instance to check that NAT is working

### Conclusion
Setting up jump hosting with NAT in AWS allows for secure access to resources within private subnets. By following the steps outlined in this guide, you can establish a secure network architecture that facilitates controlled access to your AWS resources.



