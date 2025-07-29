# Deploying DeepSeek-R1 1.5B on Huawei Cloud Using Ollama

## Objective:
This lab guides you through the step-by-step process of deploying the DeepSeek-R1 1.5B large language model on Huawei Cloud by setting up an ECS instance and using the Ollama tool for local model management and inference.

## 1. Prerequisites

Access to Huawei Cloud Lab Desktop using the provided exercise account.

Internet connection for downloading resources.

Tip: Use the IAM user credentials and refresh the lab page if needed to ensure you're logged into the Huawei Cloud console.

## 2. Preparing the Lab Environment

### 2.1 Creating an ECS Instance

- Log in to Huawei Cloud Console.

- Navigate to Elastic Cloud Server (ECS) via the service list or by searching "ECS".

- Click Buy ECS > Select Custom Config.

Set the following:

- Billing Mode: Pay-per-use

- Region: AP-Singapore

- Architecture: x86

Flavor: c6.xlarge.2 (4 vCPUs, 8 GiB)

- Image: CentOS 8.2 64bit (40 GiB)

- System Disk: Default (40 GB)

Configure the Network:

VPC and Security Group: Use default (or create if not present)

- EIP: Auto assign

- EIP Type: Dynamic BGP

- Bandwidth: 100 Mbit/s

Set the instance name and password:

- ECS Name: ecs-cent

- Password: Huawei1234%

- Click Submit, then Agree and Submit to launch the instance.

### 2.2 Logging In to ECS

Use CloudShell to connect.

Enter the password Huawei1234%.

## 3. Installing Ollama

Ollama allows local deployment and interaction with large language models. You can install it via GitHub or a backup OBS source.

#### Solution 1: Install via GitHub

curl -fsSL https://ollama.com/install.sh | sh
ollama -v

If the GitHub download fails, use Solution 2.

#### Solution 2: Install via Huawei Cloud OBS Backup

wget https://sandbox-experiment-files.obs.cn-north-4.myhuaweicloud.com/deepseek/ollama-linux-amd64.tgz
sudo tar -C /usr -xzf ollama-linux-amd64.tgz
sudo chmod +x /usr/bin/ollama

Check if user ollama exists:

id ollama

If not, create it:

sudo useradd -r -s /bin/false -m -d /usr/share/ollama ollama

Create the service file:

cat << EOF > /etc/systemd/system/ollama.service
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
ExecStart=/usr/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3

[Install]
WantedBy=default.target
EOF

Enable and start the service:

sudo systemctl daemon-reload
sudo systemctl enable ollama
sudo systemctl start ollama
ollama -v

## 4. Deploying DeepSeek-R1 1.5B Model

#### Solution 1: Pull from Ollama Registry

ollama pull deepseek-r1:1.5b
ollama run deepseek-r1:1.5b

If download speed is slow or interrupted, press Ctrl+C and retry. Resumable downloads are supported.

#### Solution 2: Download Model from OBS

wget https://sandbox-experiment-files.obs.cn-north-4.myhuaweicloud.com/deepseek/ollama_deepseek_r1_1.5b.tar.gz
sudo tar -C /usr/share/ollama/.ollama/models -xzf ollama_deepseek_r1_1.5b.tar.gz
cd /usr/share/ollama/.ollama/models
mv ./deepseek/sha256* ./blobs
mkdir -p ./manifests/registry.ollama.ai/library/deepseek-r1
mv ./deepseek/1.5b ./manifests/registry.ollama.ai/library/deepseek-r1
rm -rf deepseek/
ollama list
ollama run deepseek-r1:1.5b
 Now you're ready to interact with the DeepSeek model. If responses are inaccurate, use /bye to reset the session.

 <img width="1333" height="597" alt="ecs" src="https://github.com/user-attachments/assets/e23a08fc-1aab-4858-8bb6-88abc1ee4dd8" />

 <img width="955" height="301" alt="ollama" src="https://github.com/user-attachments/assets/07cc5376-21f3-46c2-ab9a-3fa45b71354b" />

 <img width="527" height="242" alt="root" src="https://github.com/user-attachments/assets/8abdcd24-8613-4f3f-b6bd-870930e4e7ca" />
 


