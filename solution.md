# AWS Application Load Balancer – Solution Guide

## Step 1: Launch EC2 Instances

AMI: Amazon Linux
Instance Count: 2

### User Data Script

#!/bin/bash
yum update -y
yum install httpd -y
service httpd start
chkconfig httpd on
cd /var/www/html
echo "This is server-1" > index.html

Launch instances.

---

## Step 2: Configure Security Group

- Edit Inbound Rules
- Allow HTTP (Port 80)
- Source: 0.0.0.0/0
- Rename Security Group to: ELB

---

## Step 3: Rename Instances

- Rename instance 1 → server-1
- Rename instance 2 → server-2

Update server-2 content:

cd /var/www/html
sudo vi index.html
Change text to: This is server-2

---

## Step 4: Create Target Group

- Target Type: Instances
- Name: my-target-group
- Register both EC2 instances
- Wait until instances show Healthy

---

## Step 5: Create Application Load Balancer

- Type: Application Load Balancer
- Name: myapplication-LB
- Scheme: Internet-facing
- Availability Zones: Select at least two
- Security Group: Select ELB security group
- Target Group: Select previously created target group

Create Load Balancer.

---

## Step 6: Validate Load Balancing

- Go to Load Balancer
- Copy DNS name
- Paste into browser

Refresh multiple times.
You should see:

- This is server-1
- This is server-2

Traffic will distribute between both servers.

---

## ✅ Outcome

Successfully implemented:

- Application Load Balancer
- Target Group with health checks
- Load distribution between two EC2 instances

------------------------------------------------------------------------

## 👨‍💻 Author

Rushikesh Sutar\
DevOps Engineer

Focused on Production-Ready Git Practices

------------------------------------------------------------------------

⭐ If this repository helped you, consider giving it a star.

