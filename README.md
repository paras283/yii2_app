## Infrastructure Automation (Ansible)

This project uses Ansible to configure an EC2 instance and deploy a Yii2 PHP app using Docker Swarm.



## Setup Instructions

### 1. Launch EC2 Instance

- Use Ubuntu 22.04 AMI
- Allow SSH (port 22) and HTTP (port 80) in the security group
- Download the `.pem` SSH key

### 2. Clone This Repository Locally

bash
git clone https://github.com/paras283/yii2_app.git
cd yii2_app/ansible

### 3. Configure Ansible Inventory

Update the inventory file:

[webserver]
<ec2-public-ip> ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/your-key.pem

### 4. Run Ansible Playbook

ansible-playbook -i inventory playbook.yml



### This will :

1. Install Docker, Compose, NGINX, PHP

2. Configure NGINX as a reverse proxy

3. Clone the Yii2 app repo

4. Deploy it via Docker Swarm


## Steps to Test the Deployment

### 1. SSH into the EC2 Instance

ssh -i ~/.ssh/your-key.pem ubuntu@<ec2-ip>

### 2. Check Docker Services

docker service ls

### 3. Check App in Browser

http://<ec2-public-ip>

You should see the Yii2 application home page.



## CI/CD Pipeline (GitHub Actions)

1. The GitHub Actions workflow:

2. Triggers on push to main

3. Builds and pushes Docker image to Docker Hub

4. SSHs into the EC2 server

5. Pulls the new image

6. Updates the Docker Swarm service

## Secrets used:

1. USERNAME

2. PRIVATE_KEY

3. HOST

4. DOCKER_USERNAME

5. DOCKER_PASSWORD

## Assumptions Made:

1. EC2 is already provisioned (Ansible does not create cloud resources)

2. NGINX runs on the host (not inside Docker)

3. Yii2 application is already container-ready

4. Repo is public or GitHub token is configured for private access

5. Docker image uses port 8080 internally, and NGINX proxies to it
