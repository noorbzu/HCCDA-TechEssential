# LAB: Deploying an Enterprise Web on Huawei Cloud
## Introduction
In today’s digital landscape, enterprises rely on robust, scalable, and secure infrastructure to deploy their web applications. Cloud computing offers the flexibility and tools required to meet these demands. This lab focuses on deploying an enterprise-level website on Huawei Cloud, utilizing key services such as Elastic Cloud Server (ECS), Relational Database Service (RDS), Elastic Load Balancer (ELB), and Auto Scaling (AS). The architecture follows a distributed model with separate nodes for web and database services to ensure performance, availability, and scalability.

## 1. Environment Setup and Initial Configuration

### 1.1 Creating a Virtual Private Cloud (VPC)
To begin, a Virtual Private Cloud (VPC) was created in the AP-Singapore region to establish a secure and isolated network. A subnet and related resources were automatically provisioned during the VPC creation.

### 1.2 Configuring a Security Group
A custom security group was created and configured with an inbound rule allowing all traffic from IP address 0.0.0.0/0. This setup enables open access for testing purposes, which can later be restricted as needed.

## 2. Provisioning Core Cloud Resources
   
### 2.1 Creating an ECS Instance (Web Server Node)
An Elastic Cloud Server (ECS) was purchased with the following specs:

**Billing Mode: Pay-per-use**

**OS: CentOS 7.6 (64-bit)**

**Instance Type: 1 vCPU, 1 GB RAM**

**Login Method: Password-based**

**Network: Attached to previously created VPC and security group**

**Elastic IP (EIP): Assigned automatically**

This ECS will act as the web server node for hosting the enterprise website.

### 2.2 Buying an RDS Instance (Database Node)
A Relational Database Service (RDS) instance running MySQL 8.0 was deployed using:

**Instance Type: 2 vCPU, 4 GB RAM**

**Storage: Cloud SSD**

**Deployment Mode: Primary/Standby**

**Network and Security: Integrated with the created VPC and security group**

This RDS instance will serve as the backend database server for the website.

## 3. Setting Up LAMP and WordPress
   
### 3.1 LAMP Stack Installation
The following software packages were installed on the ECS to set up the LAMP stack:
**Code**
bash
Copy
Edit
yum install -y httpd php php-fpm php-mysql mysql
After configuring the Apache (httpd.conf) and downloading WordPress, the files were extracted to /var/www/html/ and given appropriate permissions. Services httpd and php-fpm were started and set to launch on boot.

### 3.2 Creating the WordPress Database
Using the RDS MySQL console, a database named wordpress was created via SQL query:

sql
Copy
Edit
CREATE DATABASE wordpress;

### 3.3 WordPress Installation
The WordPress setup wizard was accessed via browser using the ECS EIP. The necessary database credentials, including the floating IP of the RDS instance, were entered to complete the setup.

## 4. Implementing High Availability with ELB and AS
   
### 4.1 Creating a Shared Load Balancer
An Elastic Load Balancer (ELB) was deployed and configured with:

**Type: Shared, Public**

**Network: Connected to the existing VPC**

**Listener: Configured to forward HTTP traffic to backend servers**

**Health Check: Disabled for manual verification**

### 4.2 Creating a System Image
A private image of the configured ECS was created to automate ECS replication. This image will be used by Auto Scaling to generate identical ECS instances dynamically.

### 4.3 Configuring Auto Scaling (AS)
An AS group was created using the ECS image, and the load balancer was integrated. Two policies were added to manage scaling:

Scale-out: CPU ≥ 60% → Add 1 instance

Scale-in: CPU ≤ 20% → Remove 1 instance

Within minutes, new ECS instances were automatically added to the backend server group, confirming that Auto Scaling was functioning correctly.

## 5. Website Access and Monitoring
### 5.1 Accessing the Website
The website was accessed successfully using the public EIP of the load balancer, confirming the LAMP setup, load distribution, and database integration were all working.

### 5.2 Monitoring with Cloud Eye
Using Huawei Cloud’s Cloud Eye, resource usage statistics and alarms for ECS and RDS were monitored. This feature helps in identifying potential issues and optimizing performance.


<img width="1047" height="552" alt="login page" src="https://github.com/user-attachments/assets/41a421db-dc4b-4c2d-95d5-3ee2e9e69b12" />



<img width="1646" height="476" alt="vpc" src="https://github.com/user-attachments/assets/5d83d4b9-113f-446b-85ff-c096845cbef6" />



<img width="1640" height="485" alt="security group created" src="https://github.com/user-attachments/assets/5f4355d3-d0c0-4767-a7de-c0e8069ae904" />




