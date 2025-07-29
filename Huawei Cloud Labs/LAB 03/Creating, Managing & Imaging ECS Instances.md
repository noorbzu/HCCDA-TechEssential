# Creating, Managing & Imaging ECS Instances
This lab focused on deploying and managing Elastic Cloud Servers (ECS) in Huawei Cloud. 
The tasks included provisioning Windows and Linux virtual machines, adjusting their specifications, and creating private system disk images for future reuse. 
The goal was to gain hands-on experience with cloud computing services and image management using Huawei’s platform.

## What is the Lab Desktop?
The Lab Desktop is a pre-configured virtual environment that allows users to safely access Huawei Cloud services. It provides a controlled space where users can perform cloud labs without affecting personal accounts or local environments.

### Creating ECS Instances (Windows & Linux)
####  Step 1: Creating a VPC
A Virtual Private Cloud (VPC) was created in the AP-Singapore region:

**VPC Name: vpc-Sandbox-<username>**

CIDR Block: 192.168.0.0/16

Subnet Name: subnet-Sandbox-<username>

Subnet CIDR Block: 192.168.0.0/24

This isolated network provided the foundation for secure instance deployment.

#### Step 2: Creating a Windows ECS
A Windows ECS was provisioned with the following:

Billing Mode: Pay-per-use

Flavor: General computing (2 vCPUs, 4 GB RAM)

Image: Windows Server 2012 R2 Standard 64-bit

System Disk: 40 GB, High I/O

Login Mode: Password

EIP & Security: Auto-assigned public IP with host security enabled

#### Step 3: Creating a Linux ECS
Similarly, a Linux instance was launched:

Image: CentOS 7.6 64-bit

Login Mode: Password

Access: VNC via console (no external EIP attached)

### 1.2 Logging into ECS Instances
Windows ECS: Accessed using VNC from the console and logged in via Ctrl+Alt+Del.

Linux ECS: Logged in as root using the VNC console:

makefile
Copy
Edit
Login: root  
Password: Huawei@123
### 1.3 Modifying Windows ECS Specifications
To simulate scaling, I stopped the Windows ECS and modified its memory from 4 GB to 8 GB. After resizing, the ECS status changed to Resized, and upon restarting, the new configuration was active.
 ## 2. Creating a Windows System Disk Image
### 2.1 Preparation Before Imaging
Enabled DHCP and Remote Desktop

Configured Windows Firewall to allow remote access

Verified that Cloudbase-Init was pre-installed

### 2.2 Creating the Image
Service: Image Management

Source ECS: ecs-windows

Image Name: image-windows2012

Image creation took ~15 minutes. Status: Normal

### 2.3 Renaming & 2.4 Copying the Image
The image was renamed and its description updated.

Then, it was replicated to another region. KMS encryption was not used.
###  2.5 Creating ECS from the Custom Image
A new ECS was successfully launched using the private Windows image, confirming that the pre-installed configurations were preserved.

 ## 3. Creating a Linux Private Image
###  3.1 Preparation Before Imaging
Verified DHCP by editing:

swift
Copy
Edit
/etc/sysconfig/network-scripts/ifcfg-eth0
Checked required packages:

bash
Copy
Edit
ls -lh /Cloud*
rpm -qa | grep cloud-init
Removed network rules:

bash
Copy
Edit
ls -l /etc/udev/rules.d
### 3.2 Creating the Linux Image
Source ECS: ecs-linux

Image Name: image-centos7.6

Image status changed to Normal upon successful creation.

### 3.3 Sharing the Private Image
Retrieved Project ID from My Credentials

Used Image Management Service to share the image with another user

### 3.4 Managing Image Tenants
Added a tenant by entering their Project ID

If needed, tenants could be removed and re-added for re-sharing

<img width="895" height="565" alt="lab 333" src="https://github.com/user-attachments/assets/ff00d66e-0a6f-4378-a8de-93a2e79ccf3d" />

<img width="883" height="487" alt="save thus" src="https://github.com/user-attachments/assets/2788df0f-d294-450e-8c44-75324623b418" />

<img width="822" height="408" alt="request" src="https://github.com/user-attachments/assets/2367cdb2-4b15-418d-8a05-0c4ee4a88f38" />

<img width="672" height="257" alt="root lab 2" src="https://github.com/user-attachments/assets/4f009e74-be7d-4ac6-8735-09a8d6a00607" />

<img width="680" height="75" alt="hello sfs" src="https://github.com/user-attachments/assets/3d9322f5-00d7-4339-a828-2246199d8d7e" />

<img width="902" height="191" alt="crested" src="https://github.com/user-attachments/assets/df45706c-0cf6-4bb7-a802-9959fedd8e15" />





