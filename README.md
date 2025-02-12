# AWS-Three-Tier-Web-Architecture
This project implements a Three-Tier Architecture on AWS, consisting of a web server, application server, and an Amazon RDS database. The infrastructure is manually configured to ensure scalability, security, and high availability. It includes setting up VPC networking, subnets, security groups, and other essential AWS services like Elastic Load Balancer and Auto Scaling to support a robust and fully functional deployment.
# Architecture Overview
![Architecture](https://github.com/user-attachments/assets/f24552f9-2c5d-461c-8e95-56f24b38171c)

# Creating 3 Tier Architecture & Integrating Other AWS Resources
**Step 1: Download Code from GitHub in Your Local System**

**Step 2: Create Two S3 Buckets**<br>

![image](https://github.com/user-attachments/assets/fe1ad413-a610-4a06-bce3-8b572c4e4f65)

- Create one S3 bucket for storing web-server & app-server code.


- Create another S3 bucket for VPC flow logs.


Step 3: Create IAM Role with Policies<br>
- S3 read only.
- SSM managed instance core.

Step 4: Create VPC, Subnets, IGW, NAT-GW, RT<br>
- Enable auto-assign public IP for web-tier public subnets.
- Create flow logs for VPC & use the S3 bucket created above.

Step 5: Create Security Groups<br>
- External-Load-Balancer-SG --> HTTP (80): 0.0.0.0/0.
- Web-Tier-SG --> HTTP --> Ext-LB-SG.
- Internal-Load-Balancer-SG --> HTTP --> Web-Tier-SG.
- App-Tier-SG --> Port 4000 --> Internal-LB-SG.
- DB-Tier-SG --> MySQL (3306) --> App-Tier-SG.

Step 6: Create DB Subnet Group & RDS<br>
- Create DB subnet group.
- Create RDS - Multi-AZ.
- Place them in DB subnet group created above.

Step 7: Create SNS for both App server and web server.<br>
