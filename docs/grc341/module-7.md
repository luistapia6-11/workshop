# Objective
In this module we will provision and configure our instance(s) to receive the files necessary for the Ansible playbook to run.

## Prerequisites

1. Ensure you are logged into an AWS account with admin access
2. Completed all previous modules
3. SSH Client to remote into your linux instance(s)
4. Existing VPC with public/private subnets and outbound internet access

## Provision Red Hat Enterprise Linux 7 instance

1. Navigate to the <a href="https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#LaunchInstanceWizard:" target="_blank">marketplace</a> and search for ```Linux 7```
2. Select ```Red Hat Enterprise Linux (RHEL) 7 (HVM)```
3. On ```Step 2: Choose an Instance Type``` select ```t2.micro```
4. On ```Step 3: Configure Instance Details``` provision the instance in a subnet that you have access to
5. For ```IAM role``` select the IAM role created in Setting up supporting infrastructure
6. On ```Step 5: Add Tags``` add the following tag ```Key:Deploy``` ```Value:CIS```. CodeDeploy will use these tags to target instances to deploy the Ansible playbook
7. On ```Step 6: Configure Security Group``` configure SSH access
8. Launch your instance(s)

**Note**: _Ideally we would provision the instance in a private subnet and connect over VPN. If you do not have a VPN configured for your VPC, you can provision the instance in a public subnet for this workshop. Make sure to lockdown SSH access to just your device._

## Configure instance(s)

1. First, we need to update our instance(s)

        sudo yum update -y

2. Install epel-repo

        sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

3. Install pip

        sudo yum install wget -y
        sudo wget https://bootstrap.pypa.io/get-pip.py
        sudo python get-pip.py

4. Install Ansible

        sudo pip install ansible

5. Install AWS cli

        sudo pip install awscli

6. Install SSM agent

        sudo yum install -y https://s3.amazonaws.com/ec2-downloads-windows/SSMAgent/latest/linux_amd64/amazon-ssm-agent.rpm

7. Install CodeDeploy agent

        sudo yum install -y ruby
        cd /home/ec2-user
        sudo wget https://aws-codedeploy-us-east-1.s3.amazonaws.com/latest/install
        sudo chmod +x ./install
        sudo ./install auto

8. Make sure SSM and CodeDeploy agents are running

        sudo systemctl status amazon-ssm-agent
        sudo service codedeploy-agent status

The instance is now configured with Ansible, SSM and CodeDeploy agents and is ready to receive and run the ansible playbook from the reinforce-demo artifacts.