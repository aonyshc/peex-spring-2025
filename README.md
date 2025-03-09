# This is a DevOps pet project, as a preparation part to PeEx spring 2025

## Provision infrastructure on AWS with Terraform
### This project contains terraform configuration files on creating EC2 and RDS instances inside a Custom VPC on AWS. Here is the architecture of what will be created:

![Custom VPC architecture for AWS](https://miro.medium.com/max/700/1*Oxp7FZT4Z9RWqpnJn-hHqw.png)

## Set Up
#### Prerequisites
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) installed and configuration
- [Terraform](https://www.terraform.io/downloads) installed

#### Create the Secrets file
Create a secrets file called ***secrets.tfvars*** and populate it with the follow secrets:
  - **db_username** <-- this is going to be the master user for RDS
  - **db_password** <-- this is going to be the RDS master user's password
  - **my_ip** <-- this is going to be your public IP

## Running the Configuration
#### Initializing the Terraform directory
Run the command: `terraform init`

#### Apply the Terraform Config to AWS
Run the command: `terraform apply -var-file="secrets.tfvars"`

### To destroy everything that was created by the Terraform Config
Run the command: `terraform destroy -var-file="secrets.tfvars"`

-----
## Configure provisioned EC2 instance with Ansible
#### Prerequisites:
- Ansible installed on localhost (https://docs.ansible.com/ansible/2.9/installation_guide/intro_installation.html)

#### Add obtained with Terraform EC2 instance puplic (elastic) IP to inventory file
Edit inventory.ini with your values
`[ec2_instance] <ec2_puplic_ip> ansible_user=ubuntu ansible_ssh_private_key_file=<path_to_ec2_private_key> ansible_python_interpreter=/usr/bin/python3`

#### Run ansible playbook, which installs python3, pip, flask, clones repository with flask web app, and launches flask
`ansible-playbook -i inventory.ini setup_flask_web_app.yml`

---
## Deploy CI/CD with Jenkins (under development..)

---
Thanks to @dispact and @eeb2828, their repos were used in this project:
https://github.com/dispact/terraform-custom-vpc
https://github.com/leeb2828/Random-Quote-Generator_PY