## Infrastructure Automation (Ansible)

This project uses Ansible to configure an EC2 instance and deploy a Yii2 PHP app using Docker Swarm.

## How to Use

1. Update `inventory` with your EC2 IP and SSH key path.
2. From your local machine:, run:
```bash
cd ansible
ansible-playbook -i inventory playbook.yml


### This will :

1. Install Docker, Compose, NGINX, PHP

2. Configure NGINX as a reverse proxy

3. Clone the Yii2 app repo

4. Deploy it via Docker Swarm
