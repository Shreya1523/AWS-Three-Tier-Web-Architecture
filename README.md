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

![image](https://github.com/user-attachments/assets/d15f0b03-0248-4eb5-a012-45328b7b8ba2)

- Web-Tier-SG --> HTTP --> Ext-LB-SG.

![image](https://github.com/user-attachments/assets/cced80cc-a330-4f6a-b6e6-424f753770e0)

- Internal-Load-Balancer-SG --> HTTP --> Web-Tier-SG.

![image](https://github.com/user-attachments/assets/9ac13837-11c3-4e41-89f6-c11bcca2886f)

- App-Tier-SG --> Port 4000 --> Internal-LB-SG.

![image](https://github.com/user-attachments/assets/a9b774a1-26f8-4db0-a3d2-739d6f47f7df)

- DB-Tier-SG --> MySQL (3306) --> App-Tier-SG.

![image](https://github.com/user-attachments/assets/61a39387-9ad8-42c9-ae9a-c0d92fbef86a)

<h2>Step 6: Create DB Subnet Group & RDS</h2>

- Create DB subnet group.

![image](https://github.com/user-attachments/assets/8ddcdb33-389e-4111-bd4a-9a75dcff6e13)

- Create RDS - Multi-AZ.

![image](https://github.com/user-attachments/assets/469b1b7d-c983-472f-a324-9906c3caf983)

- Place them in DB subnet group created above.

<h2>Step 7: Create SNS for App Server and Web Server</h2>

![image](https://github.com/user-attachments/assets/8ab7015e-b228-4da6-aa8b-57b1b580aa28)

![image](https://github.com/user-attachments/assets/62b8b8e0-b2b5-47e8-a163-5c424957baab)

![image](https://github.com/user-attachments/assets/355b8a69-1899-4a67-830c-02abb627236c)

<h2>Step 8: Create Test App Server, Install Packages, Test Connections</h2>

- Test App-Server Commands

![image](https://github.com/user-attachments/assets/120c9236-29e7-4324-a016-f3bfe164a46e)

- Create AMI.

![image](https://github.com/user-attachments/assets/1b5a809b-ce97-4bf2-ba6c-51ca39292dad)

- Create launch template using AMI.

![image](https://github.com/user-attachments/assets/399a4cc9-703b-4e85-bfe6-389ac5c72f2d)

- Create target group.

![image](https://github.com/user-attachments/assets/ac695d24-0e95-46a1-b56a-1ff1bb9e4011)

- Create internal load balancer.

![image](https://github.com/user-attachments/assets/7ecb6174-cf7b-4ee1-a54c-0e4408f201a1)

- Create autoscaling group.

![image](https://github.com/user-attachments/assets/579780d0-3ae2-4a5e-8142-c023e475c407)

<h2>Step 9: Create Test Web Server, Install Packages (Nginx, Node.js (React)), Test Connections</h2>

- Test Web-Server Commands

![image](https://github.com/user-attachments/assets/df198038-0d52-4711-8236-e94b0a09bfa9)

- Create AMI.

![image](https://github.com/user-attachments/assets/e2f7f3a1-416e-49ea-8a40-d94a1aa38206)

- Create launch template using AMI.

![image](https://github.com/user-attachments/assets/28737468-46fa-4b57-a1b6-cfa9cba95cbd)

- Create target group.

![image](https://github.com/user-attachments/assets/da885129-1c4e-4e5d-b698-f558b04d0409)

- Create external load balancer.

![image](https://github.com/user-attachments/assets/9047804f-02ba-481a-a816-66a5de1d672a)

- Create autoscaling group.

![image](https://github.com/user-attachments/assets/a398b605-196b-4eb7-920d-e0bd6ca9a015)

<h2>Step 10: Add External-ALB-DNS Record in Route 53</h2>

![image](https://github.com/user-attachments/assets/d45a0ec2-8b8e-444f-930f-eaac6f17ab4f)

<h2>Step 11: Create CloudWatch Alarms Along with SNS</h2>

![image](https://github.com/user-attachments/assets/613ffcf0-754a-4728-ac0e-0bf03f85b13e)

<h2>Step 12: Create CloudTrail</h2>

![image](https://github.com/user-attachments/assets/42d87161-484f-4624-b1e8-a8a94960a9e5)

# Output

![image](https://github.com/user-attachments/assets/3d741f94-1ebf-4da9-b8dd-796371e11c9a)

<h2>Step 13: Deleting the Entire Infrastructure</h2>

- Delete CloudWatch alarms.
- Delete records from Route 53.
- Delete load balancers, target groups, ASG, launch templates.
- Delete security group.
- Delete NAT gateway (it will take 5 mins).
- Release elastic IP.
- Delete VPC.
- Delete RDS subnet group, RDS.
