# Objective
In this module we will create S3 buckets to store build artifacts and logs. We will also create an encryption key that will be used to encrypt data at rest. Lastly, we will create an IAM role that will give our ec2 instance permissions for SSM. While this should work in any commercial region, it was tested specifically in US-East-1.

## Prerequisites

1. Ensure you are logged into an AWS account with admin access
2. AWS CLI set up on the local client.

## Create IAM role

1. **Click** on the link below to launch the cloudformation template

    [us-east-1](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=reinforce-instance-role&templateURL=https://aws-reinforce-demo-grc341.s3.amazonaws.com/templates/instance-role.yml)

## Setting up S3 bucket for build artifacts

1. Login to the AWS management console
2. **Click** on the link below to launch the cloudformation template

    [us-east-1](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=reinforce-artifactbucket&templateURL=https://aws-reinforce-demo-grc341.s3.amazonaws.com/templates/artifact_bucket.yml)

3. **Click** on the link below to launch the cloudformation template

    [us-east-1](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=reinforce-artifactbucket-policy&templateURL=https://aws-reinforce-demo-grc341.s3.amazonaws.com/templates/bucket-policy.yml)

## Setting up S3 bucket for logging

1. **Click** on the link below to launch the cloudformation template

    [us-east-1](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=reinforce-loggingbucket&templateURL=https://aws-reinforce-demo-grc341.s3.amazonaws.com/templates/logging_bucket.yml)

## Create KMS Key for encryption

1. **Click** on the link below to launch the cloudformation template

    [us-east-1](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=reinforce-encryption-key&templateURL=https://aws-reinforce-demo-grc341.s3.amazonaws.com/templates/encryption.yml)