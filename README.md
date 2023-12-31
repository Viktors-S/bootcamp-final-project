# Architecture

- main.tf file houses the terraform configuration.
- nginx.yaml file houses the configuration necessary to install nginx on th EC2 instance.
- inv file houses the ansible-playbook inventory where you add your target machines public ip.
- index.html houses the nginx websites main page html code.
- update-html.yml is the github workflow wich automatically uploads your code to target EC2 instance.


# Instalation

## _Prerequisites_

- EC2 instance
- Required packages:
    1. awscli >=1.22.34
    2. ansible >=2.10.8
    3. terraform >=1.5.6

## _Instructions_
- Generate a ssh key using "ssh-keygen"
- Configure awscli using "aws configure"
    - Add your aws "Access key ID"
    - Add your aws "Secret access key"
    - Add your aws "region"
    - Add your preffered output type
- Clone this repository into your EC2 instance and navigate into it
- Run the command "terraform init" to initialize terraform
- Run the command "terraform apply" to apply the config
- Once terraform is done creating your instance note down its public ip
- Open up inv file using a text editor ("vim inv")
    - Add/change the inventory file to reflect your public ip
        - "3.76.247.97 ansible_ssh_user=ubuntu"
- Run the command "ansible-playbook nginx.yaml -i inv"
- Wait for the playbook to complete and your nginx server can be found at 
    http://YOUR_PUBLIC_IP

#### _TO CREATE A GITHUB WORKLFOW!!!_
- In github repository secrets add:
    - SSH_KEY with the value of your ec2 instances /home/ubuntu/.ssh/id_rsa file text
    - EC2_HOST with the value of your ec2 ip connection (e.g., ec2-***********.eu-central-1.compute.amazonaws.com)

## _Destroy instance_

- Run the command "terraform destroy"

After the command has completed the nginx server, security group, keypair is destroyed
