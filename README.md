# Deploy Docker and NGINX Containers on AWS EC2 via Ansible and GitHub Actions
This project automates the installation of Docker and deployment of an NGINX container on an already running AWS EC2 instance.
The entire process is triggered by a GitHub Actions workflow, using Ansible for configuration management.

## Project Structure
bash
.
├── .github
│   └── workflows
│       └── deploy.yml          # GitHub Actions workflow
├── deploy_nginx.yml            # Ansible playbook to install Docker and deploy NGINX
└── inventory.ini               # Ansible inventory with EC2 instance details

## Prerequisites
* An existing AWS EC2 instance (Ubuntu preferred)
* SSH access to the instance
* GitHub repository to store this project

## GitHub Secrets configured:

EC2_SSH_KEY: Your EC2 private SSH key content

## Setting Up GitHub Secrets
Go to your GitHub repository:

Settings ➔ Secrets and variables ➔ Actions ➔ New repository secret

### Add a new secret:

Name: EC2_SSH_KEY

Value: Paste the content of your .pem private key (used for EC2 SSH access)

## How to Trigger the Deployment
Once you push the project to GitHub:

* Go to the Actions tab in your repository.
* Select Deploy NGINX via Ansible workflow.
* Click on Run workflow.
* Wait for the job to complete.

That's it! 
The NGINX container will be deployed and accessible via your EC2 public IP on port 80.

## Key Components
* Ansible Playbook (deploy_nginx.yml)
* Installs Docker if not already present.
* Ensures Docker service is running.
* Pulls and starts an NGINX container, mapping port 80.
* GitHub Actions Workflow (deploy.yml)
* Installs Ansible on the GitHub runner.
* Sets up SSH key for Ansible.
* Executes the Ansible playbook against the EC2 instance.

## Example Access
After a successful run, you can access your NGINX server by visiting:

cpp
http://<your-ec2-public-ip>

You should see the default NGINX welcome page!

## Future Enhancements
* Use dynamic inventory for better scalability.
* Add support for multiple containers or custom images.
* Secure the playbook and workflow with better practices (vaults, encrypted secrets).

## Contributing
Feel free to fork, enhance, and submit a pull request.
Feedback, suggestions, and improvements are always welcome!