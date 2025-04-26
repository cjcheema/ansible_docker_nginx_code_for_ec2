# Deploy Docker and NGINX Containers on AWS EC2 via Ansible and GitHub Actions
This project automates the installation of Docker and deployment of an NGINX container on an already running AWS EC2 instance.
The entire process is triggered by a GitHub Actions workflow, using Ansible for configuration management.

## Project Structure
```bash
.
├── .github
│   └── workflows
│       └── deploy.yml          # GitHub Actions workflow
├── deploy_nginx.yml            # Ansible playbook to install Docker and deploy NGINX
└── inventory.ini               # Ansible inventory with EC2 instance details 
```
<b>Note:</b> I have removed the inventory file since I am using dynamic inventory with ansible considering security.

## Prerequisites
* An existing AWS EC2 instance (Ubuntu preferred)
* SSH access to the instance
* GitHub repository to store this project

## Setting Up GitHub Secrets
Go to your GitHub repository:

Settings ➔ Secrets and variables ➔ Actions ➔ New repository secret

### Configure the GitHub Secrets under New Repository secret:

* Name: EC2_SSH_KEY  
  Value: Paste the content of your .pem private key (used for EC2 SSH access)

* Name: EC2_USER<br />
  Value: Provide the EC2 instance login user in GitHub Secrets which can be used for executing the ansible playbook for deployment.

* Name: EC2_ANSIBLE_HOST<br />
  Value: Provide your EC2 machine Public IP address in GitHub secret to avoid hardcoding of IPs and keeping your virtual machine IP secure. 

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

```cpp
http://<your-ec2-public-ip>
```

You should see the default NGINX welcome page!

## Read more
Check out my article to learn more on How to Deploy Docker and NGINX Containers on AWS EC2 via Ansible and GitHub Actions:  https://www.cjcheema.com/2025/04/26/how-to-deploy-docker-containers-with-nginx-on-aws-ec2-using-ansible-and-github-actions/

## Contributing
Feel free to fork, enhance, and submit a pull request.
Feedback, suggestions, and improvements are always welcome!

## Author: 
This project is created and maintained by Charanjit Singh.

* Email: charanjit.singh@outlook.in/charanjit.cheema@cjcheema.com
* Website: https://www.cjcheema.com
* LinkedIn: https://www.linkedin.com/in/cjcheema/

Feel free to connect for any questions, suggestions, or feedback.