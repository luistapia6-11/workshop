# Objective
In this module we will update our buildspec.yml file with the artifacts bucket we created in an earlier module.

## Prerequisites

1. Ensure you are logged into an AWS account with admin access
2. Completed Setting up supporting infrastructure module
3. Laptop with an IDE and git installed

## Update buildspec.yml

1. Navigate to your local repository where you copied the contents of reinforce-demo.zip from an earlier module
2. Open buildspec.yml in your IDE
3. Edit buildspec.yml by replacing YOUR_ARTIFACTS_BUCKET_NAME with the name of the artifacts bucket created in an earlier module

         build:
           commands:
             - aws s3 cp --recursive --acl bucket-owner-full-control ./Ansible-RHEL7-CIS-Benchmarks-master/roles s3://YOUR_ARTIFACTS_BUCKET_NAME/cis-rhel-ansible-master/Ansible-RHEL7-CIS-Benchmarks-master/roles
             - aws s3 cp --acl bucket-owner-full-control ./appspec.yml s3://YOUR_ARTIFACTS_BUCKET_NAME/cis-rhel-ansible-master/appspec.yml
             - aws s3 cp --acl bucket-owner-full-control ./Ansible-RHEL7-CIS-Benchmarks-master/playbook.yml s3://YOUR_ARTIFACTS_BUCKET_NAME/cis-rhel-ansible-master/Ansible-RHEL7-CIS-Benchmarks-master/playbook.yml
             - aws s3 cp --acl bucket-owner-full-control ./Ansible-RHEL7-CIS-Benchmarks-master/ansible.cfg s3://YOUR_ARTIFACTS_BUCKET_NAME/cis-rhel-ansible-master/Ansible-RHEL7-CIS-Benchmarks-master/ansible.cfg
             - aws s3 cp --recursive --acl bucket-owner-full-control ./scripts s3://YOUR_ARTIFACTS_BUCKET_NAME/cis-rhel-ansible-master/scripts

4. Once you've updated buildspec.yml you can commit your changes to your origin