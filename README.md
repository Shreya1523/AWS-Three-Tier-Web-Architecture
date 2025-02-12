# AWS-Three-Tier-Web-Architecture
This project implements a Three-Tier Architecture on AWS, consisting of a web server, application server, and an Amazon RDS database. The infrastructure is manually configured to ensure scalability, security, and high availability. It includes setting up VPC networking, subnets, security groups, and other essential AWS services like Elastic Load Balancer and Auto Scaling to support a robust and fully functional deployment.
# Architecture Overview
![Architecture](https://github.com/user-attachments/assets/f24552f9-2c5d-461c-8e95-56f24b38171c)

# Creating 3 Tier Architecture & Integrating Other AWS Resources
<h2>Step 1: Download Code from GitHub in Your Local System</h2>

<h2>Step 2: Create Two S3 Bucket</h2>

![image](https://github.com/user-attachments/assets/fe1ad413-a610-4a06-bce3-8b572c4e4f65)

- Create one S3 bucket for storing web-server & app-server code.

![image](https://github.com/user-attachments/assets/78847c1a-8c53-4831-b4f1-fd968fcff6cb)

- Create another S3 bucket for VPC flow logs.

![image](https://github.com/user-attachments/assets/4f8b275d-7150-4088-9f15-7b43d0f9da5b)

<h2>Step 3: Create IAM Role with Policies</h2>
- S3 read only.
- SSM managed instance core.

![image](https://github.com/user-attachments/assets/3183634a-7e22-4b28-b231-1fd0412c3015)

<h2>Step 4: Create VPC, Subnets, IGW, NAT-GW, RT</h2>

![image](https://github.com/user-attachments/assets/3a94602e-94d9-448a-8040-214cfcaae73b)

![image](https://github.com/user-attachments/assets/a0488618-8f9b-4efc-9782-d8703ba2e55e)

![image](https://github.com/user-attachments/assets/0170cb2b-9df5-4a13-b588-e51d7e1e9594)

![image](https://github.com/user-attachments/assets/d9603df8-a221-49f7-9dc8-bc795a399bfa)

![image](https://github.com/user-attachments/assets/b55869bd-516e-4714-a0c7-255affc050ec)

- Enable auto-assign public IP for web-tier public subnets.

![image](https://github.com/user-attachments/assets/911ae19d-2edb-473c-82fb-f73f396c1941)

- Create flow logs for VPC & use the S3 bucket created above.

![image](https://github.com/user-attachments/assets/4f8b275d-7150-4088-9f15-7b43d0f9da5b)

<h2>Step 5: Create Security Groups</h2>
  
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
