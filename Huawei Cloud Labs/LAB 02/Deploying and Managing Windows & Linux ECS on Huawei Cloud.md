# Deploying and Managing Windows & Linux ECS on Huawei Cloud: A Hands-on Compute Service Lab

## Introduction
This article walks through a comprehensive lab exercise focused on creating, configuring, and managing Elastic Cloud Servers (ECS) using Huawei Cloud. It covers the full process of deploying both Windows and Linux ECS instances, creating private system disk images, modifying server specifications, and managing shared images. This hands-on lab is ideal for learners aiming to strengthen their practical skills in cloud infrastructure management.

### 1. Setting Up the Lab Environment

What is Lab Desktop?The Lab Desktop is a pre-configured virtual desktop environment used for lab exercises. It provides all necessary access credentials and tools, such as browsers and remote login utilities, to interact with the Huawei Cloud Console.

#### Login Instructions:

- Open Chrome on the Lab Desktop.

- Navigate to the Huawei Cloud Login Page.

- Select IAM User Login.

- Enter the lab-provided credentials (not your personal Huawei account).

### 2. Creating Elastic Cloud Servers (ECS)

#### 2.1 What is a VPC?
A Virtual Private Cloud (VPC) is an isolated network environment on the cloud that enables secure resource deployment.

##### Steps to Create a VPC:

- Region: AP-Singapore

- Go to Service List > Virtual Private Cloud > Create VPC

- VPC Name: vpc-WP (or system-assigned name)

- CIDR Block: 192.168.0.0/16, Subnet: 192.168.0.0/24

**AZ: AZ1**

*Confirm and create.*

##### Steps to Create Windows ECS:

**Go to Service List > Compute > Elastic Cloud Server > Buy ECS**

##### Basic Settings:

- Billing Mode: Pay-per-use

- Region: AP-Singapore

- CPU: x86, 2 vCPUs, 4GB RAM

- Image: Windows Server 2012 R2 (40GB)

**Host Security: Enabled**

##### Network:

- Use created VPC

- No EIP required

##### Advanced Settings:

**ECS Name: ecs-windows**

**Login: Password (Huawei@1234)**

*Confirm and Submit.*

##### Steps to Create Linux ECS:
Follow the same steps as Windows ECS, with these changes:

- Image: CentOS 7.6 64-bit

- ECS Name: ecs-linux

- EIP: Auto Assign

#### 3. Logging In to ECS

##### Windows ECS:

On the ECS dashboard, click Remote Login > Log In.

Use Send CtrlAltDel, enter the password.

##### Linux ECS:

Use Remote Login (VNC) due to no EIP.

Login as root, enter password Huawei@123 (entered in ciphertext).

#### 4. Modifying ECS Specifications

Stop the Windows ECS if running.

- Select ECS > More > Modify Specifications.

- Change RAM from 4GB to 8GB.

- Confirm changes and start ECS again.

#### 5. Creating System Disk Image from ECS

Windows ECS Configuration:

- Enable DHCP under network settings.

- Allow Remote Desktop via firewall.

- Ensure Cloudbase-Init is installed (pre-installed in public images).

##### Steps to Create Windows Private Image:

- Go to Compute > Image Management Service > Create Image

- Select Source: ecs-windows, Name: image-windows2012

- Submit and wait (10-20 minutes)

##### 6. Creating a Linux Private Image

- Linux ECS Configuration:

- Ensure DHCP is enabled in /etc/sysconfig/network-scripts/ifcfg-eth0

**Check and ensure:**

CloudResetPwdAgent is installed

Cloud-Init is installed (use rpm -qa | grep cloud-init)

No network rule files in /etc/udev/rules.d

##### Steps to Create Linux Private Image:

- Go to Image Management Service > Create Image

- Select Source: ecs-linux, Name: image-centos7.6

- Submit and wait

#### 7. Image Management and Sharing

- Sharing an Image:

- Get Project ID: Log in with personal Huawei account > My Credentials > AP-Singapore Project ID

- In SandBox console: Go to Private Image > More > Share > Enter Project ID > Confirm

#### Accepting a Shared Image:

- Log in with your Huawei account

- Go to IMS > Shared Images tab > Accept

#### Add Tenants to Shared Images:

In SandBox console > Image name > Shared with Tenants > Add Tenant

*Enter Project ID and Confirm*


<img width="680" height="192" alt="lab 2 1" src="https://github.com/user-attachments/assets/ee750941-484f-47ea-882d-355fb75688ea" />

<img width="675" height="400" alt="administrator" src="https://github.com/user-attachments/assets/84395251-3bbb-4202-877a-7cc21f3014f2" />

<img width="672" height="257" alt="root lab 2" src="https://github.com/user-attachments/assets/66e2e36e-9157-4980-8d1a-b13a6d1ed193" />

<img width="676" height="353" alt="tenant nme" src="https://github.com/user-attachments/assets/111b7be4-c227-46af-abd9-16f0f10f5875" />

<img width="681" height="526" alt="last image" src="https://github.com/user-attachments/assets/16ae44b7-0c96-446a-bf36-9f5ebcdefaba" />



