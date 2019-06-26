# Objective
In this module we will create <a href="https://aws.amazon.com/s3/" target="_blank">S3</a> buckets to store build artifacts and logs. We will also create an encryption key that will be used to encrypt data at rest. Lastly, we will create an <a href="https://aws.amazon.com/iam/" target="_blank">IAM</a> role that will give our <a href="https://aws.amazon.com/ec2/" target="_blank">EC2</a> instance permissions for <a href="https://aws.amazon.com/systems-manager/" target="_blank">AWS Systems Manager</a>. While this should work in any commercial region, it was tested specifically in US-East-1.

## Prerequisites

1. Ensure you are logged into an AWS account with admin access
2. AWS CLI set up on the local client.

## Create IAM role
We need to create a role for our instance so that it can download the <a href="https://www.ansible.com/" target="_blank">Ansible</a> playbook from our artifacts bucket later.

1. **Click** on the link below to launch the cloudformation template

    <a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=reinforce-instance-role&templateURL=https://aws-reinforce-demo-grc341.s3.amazonaws.com/templates/instance-role.yml" target="_blank">us-east-1</a>

2. Provide a name for your role

![Role Name](./images/role-name.PNG)

## Setting up S3 bucket for build artifacts
We will create an <a href="https://aws.amazon.com/s3/" target="_blank">S3</a> bucket to store our artifacts. This will be used by <a href="https://aws.amazon.com/codebuild/" target="_blank">AWS CodeBuild</a> to store our build artifacts. The instance will reference this bucket later to download the <a href="https://www.ansible.com/" target="_blank">Ansible</a> playbook. Make sure to fill in all of the parameters.

**NOTE**: _S3 bucket names are globally unique. If you get an error that a bucket already exists try a new name_

1. **Click** on the link below to launch the cloudformation template

    <a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=reinforce-artifactbucket&templateURL=https://aws-reinforce-demo-grc341.s3.amazonaws.com/templates/artifact_bucket.yml" target="_blank">us-east-1</a>


![Artifacts Bucket](./images/artifacts-bucket.PNG)

In this step we are creating an S3 bucket policy and applying it to the bucket created in the previous step. This will grant the role created earlier access to download the artifacts. Make sure to fill in all of the parameters. The parameters ```ArtifactsBucketName``` and ```S3Bucket``` must match the name of the artifacts bucket created earlier. ```RolePrincipal``` must match the name of the IAM role created earlier.

2. **Click** on the link below to launch the cloudformation template

    <a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=reinforce-artifactbucket-policy&templateURL=https://aws-reinforce-demo-grc341.s3.amazonaws.com/templates/bucket-policy.yml" target="_blank">us-east-1</a>

![Artifacts Bucket Policy](./images/artifacts-policy.PNG)

## Setting up S3 bucket for logging

We will now create an S3 bucket to store logs for troubleshooting purposes. If we encounter errors the logs may help us identify what went wrong. Make sure to fill in all of the parameters.

**NOTE**: _S3 bucket names are globally unique. If you get an error that a bucket already exists try a new name_

1. **Click** on the link below to launch the cloudformation template

    <a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=reinforce-loggingbucket&templateURL=https://aws-reinforce-demo-grc341.s3.amazonaws.com/templates/logging_bucket.yml" target="_blank">us-east-1</a>

![Logging Bucket](./images/logging-bucket.PNG)

## Create KMS Key for encryption

Here we will create a KMS encryption key that will be used by CodeBuild to encrypt our build artifacts in S3. Make sure to replace ```user/$user``` with the name of the IAM user created earlier. 

1. **Click** on the link below to launch the cloudformation template

    <a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=reinforce-encryption-key&templateURL=https://aws-reinforce-demo-grc341.s3.amazonaws.com/templates/encryption.yml" target="_blank">us-east-1</a>

![KMS Key](./images/kms.PNG)