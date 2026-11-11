# 🚀 AWS Capstone Project – Highly Available Application

## DevOps Winter Arc | Day 29/90

A hands-on AWS Capstone project focused on building a **Highly Available and Scalable Web Application** using AWS infrastructure services.

The project demonstrates how to deploy an application across multiple Availability Zones using an Application Load Balancer (ALB), EC2 Auto Scaling Group, Amazon RDS, and Amazon CloudWatch.

---

## 🎯 Project Objective

The objective of this project is to build a highly available AWS application that distributes incoming traffic across multiple EC2 instances and automatically scales infrastructure based on demand.

The architecture is designed to improve availability, scalability, fault tolerance, and application monitoring.

## 🏗️ AWS Architecture

**Application Traffic Flow:**

Users → Application Load Balancer → Auto Scaling Group → EC2 Instances → Amazon RDS

The architecture includes:

- One existing VPC distributed across two Availability Zones.
- Public subnets for the Application Load Balancer.
- EC2 instances deployed across multiple Availability Zones.
- Auto Scaling Group to maintain application capacity.
- Private database connectivity using Amazon RDS.
- CloudWatch for infrastructure monitoring.

## ☁️ AWS Services Used

| AWS Service | Purpose |
|---|---|
| Amazon VPC | Network infrastructure |
| Public Subnets | Host the Application Load Balancer |
| Private Subnets | Isolate application/database resources |
| EC2 | Host the web application |
| Launch Template | Define EC2 instance configuration |
| Auto Scaling Group | Automatically manage EC2 capacity |
| Application Load Balancer | Distribute incoming traffic |
| Target Group | Register and monitor EC2 instances |
| Amazon RDS | Managed relational database |
| Amazon CloudWatch | Monitor infrastructure metrics |
| Security Groups | Control network traffic |

## 🛠️ Implementation Steps

### 1. Existing VPC Configuration
- Used an existing VPC.
- Configured networking across two Availability Zones.
- Verified subnet and routing configurations.

### 2. Security Group Configuration
Created security groups to control communication between application components.

- ALB Security Group: Allow HTTP traffic on port 80.
- Application Security Group: Allow HTTP traffic from the ALB.
- Database Security Group: Allow database traffic only from the authorized application security group.

### 3. Launch Template Creation
- Created an EC2 Launch Template.
- Selected Amazon Linux AMI.
- Configured instance type.
- Added an Nginx installation and bootstrap script using User Data.
- Configured the required security group and instance settings.

### 4. Auto Scaling Group Configuration
Created an Auto Scaling Group using the Launch Template.

**Scaling Configuration:**

| Setting | Value |
|---|---:|
| Minimum Capacity | 2 |
| Desired Capacity | 2 |
| Maximum Capacity | 4 |
| Availability Zones | 2 |
 
The Auto Scaling Group maintains the desired EC2 capacity and can launch or terminate instances based on scaling requirements.

### 5. Application Load Balancer
- Created an Application Load Balancer.
- Configured it across public subnets.
- Created a Target Group.
- Configured HTTP traffic on port 80.
- Configured the health check path as `/`.
- Registered the EC2 instances through the Auto Scaling Group.

### 6. High Availability Validation
- Verified EC2 instances across two Availability Zones.
- Checked Target Group health.
- Confirmed both instances were healthy.
- Accessed the application using the ALB DNS name.
- Verified that requests were served by different EC2 instances.
- Tested application availability and failover behavior.

### 7. CloudWatch Monitoring
Configured Amazon CloudWatch to monitor infrastructure performance.

**Monitored Metrics:**
- CPU Utilization
- EC2 instance performance
- Application availability
- HTTP 5XX errors

Used CloudWatch metrics to observe application performance and identify infrastructure issues.

### 8. AWS CLI Verification

Used AWS CLI to inspect Target Group health:

```bash
aws elbv2 describe-target-health \
  --target-group-arn <TARGET_GROUP_ARN>
```

Verified that registered targets reported a healthy state.

Tested the application through the ALB:

```bash
curl http://<ALB-DNS-NAME>
```

Repeated requests to verify traffic distribution across different EC2 instances.

---

## 📊 Project Validation

| Component | Validation |
|---|---|
| VPC | Existing VPC verified |
| Security Groups | Configured |
| Launch Template | Created |
| Auto Scaling Group | Min: 2, Desired: 2, Max: 4 |
| Application Load Balancer | Active |
| Target Group | 2/2 Healthy |
| Multi-AZ | Two Availability Zones |
| CloudWatch | CPU monitoring verified |
| Load Balancing | Requests served by different instances |

## 🔐 High Availability Features

- Multi-AZ EC2 deployment.
- Application Load Balancer for traffic distribution.
- Auto Scaling for dynamic capacity management.
- Health checks for unhealthy instance detection.
- Private database connectivity.
- CloudWatch monitoring for infrastructure visibility.

## 💰 Cost Optimization

- Used a small instance type suitable for learning and testing.
- Configured minimum and desired capacity to control EC2 costs.
- Used Auto Scaling to adjust capacity when required.
- Monitored resource utilization through CloudWatch.
- Planned infrastructure cleanup after testing.

**Note:** ALB, EC2, RDS, NAT Gateway, and other provisioned resources may incur charges even when traffic is low. Review AWS pricing before deployment.

## 📚 Key Learnings

Through this project, I gained practical experience with:

- AWS High Availability Architecture.
- Application Load Balancer configuration.
- EC2 Launch Templates.
- Auto Scaling Groups.
- Multi-AZ deployment.
- Target Group health checks.
- AWS CLI commands.
- CloudWatch monitoring.
- Load balancing and failover concepts.
- AWS security group configuration.

## 🚀 Future Improvements

- Configure CloudWatch alarms and SNS notifications.
- Implement CPU-based scaling policies.
- Enable HTTPS using AWS Certificate Manager.
- Integrate RDS with the application.
- Configure automated deployment using CI/CD.
- Improve monitoring with custom dashboards.

## 👩‍💻 Author

**Pooja Thakare**

DevOps Winter Arc – 90 Days Challenge

Learning AWS | Linux | Docker | Kubernetes | Jenkins | Terraform

---

⭐ If you find this project useful, feel free to explore the repository and share your feedback!

#AWS #DevOps #CloudComputing #EC2 #ALB #AutoScaling #VPC #RDS #CloudWatch #HighAvailability #90DaysChallenge