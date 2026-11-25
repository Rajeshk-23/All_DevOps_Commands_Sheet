# AWS CLI Cheatsheet

> The AWS CLI manages Amazon Web Services resources from the command line.

## Table of Contents
- [Configuration & Auth](#configuration--auth)
- [EC2](#ec2)
- [S3](#s3)
- [IAM](#iam)
- [VPC & Networking](#vpc--networking)
- [Lambda](#lambda)
- [CloudFormation](#cloudformation)
- [ECS & EKS](#ecs--eks)
- [RDS](#rds)
- [CloudWatch & Logs](#cloudwatch--logs)
- [STS](#sts)

## Configuration & Auth

| Command | Description |
| --- | --- |
| `aws configure` | Configure the default profile credentials and region. |
| `aws configure list` | Display the active configuration values and sources. |
| `aws configure list-profiles` | List locally configured CLI profiles. |
| `aws configure set region us-east-1 --profile dev` | Set a profile-specific default region. |
| `aws configure get region --profile dev` | Read a profile configuration value. |
| `aws sso login --profile company` | Authenticate a profile through IAM Identity Center. |

## EC2

| Command | Description |
| --- | --- |
| `aws ec2 describe-instances` | List EC2 instances and their current state. |
| `aws ec2 run-instances --image-id ami-0123456789abcdef0 --instance-type t3.micro --count 1` | Launch an instance from an AMI. |
| `aws ec2 start-instances --instance-ids i-0123456789abcdef0` | Start one or more stopped instances. |
| `aws ec2 stop-instances --instance-ids i-0123456789abcdef0` | Stop one or more running instances. |
| `aws ec2 terminate-instances --instance-ids i-0123456789abcdef0` | Permanently terminate an instance. |
| `aws ec2 describe-images --owners self` | List AMIs owned by the current account. |

## S3

| Command | Description |
| --- | --- |
| `aws s3 ls` | List S3 buckets accessible to the current identity. |
| `aws s3 ls s3://my-bucket/` | List objects at a bucket prefix. |
| `aws s3 cp file.txt s3://my-bucket/` | Upload a local file to S3. |
| `aws s3 cp s3://my-bucket/file.txt .` | Download an S3 object locally. |
| `aws s3 sync ./site s3://my-bucket/site/` | Synchronize a local directory to S3. |
| `aws s3 rm s3://my-bucket/old.txt` | Delete an S3 object. |

## IAM

| Command | Description |
| --- | --- |
| `aws iam list-users` | List IAM users in the account. |
| `aws iam create-user --user-name deployer` | Create an IAM user. |
| `aws iam list-roles` | List IAM roles in the account. |
| `aws iam get-role --role-name AppRole` | Retrieve an IAM role and its trust policy. |
| `aws iam attach-role-policy --role-name AppRole --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess` | Attach a managed policy to a role. |
| `aws iam list-attached-role-policies --role-name AppRole` | List managed policies attached to a role. |

## VPC & Networking

| Command | Description |
| --- | --- |
| `aws ec2 describe-vpcs` | List VPCs in the selected region. |
| `aws ec2 describe-subnets` | List available subnets. |
| `aws ec2 describe-route-tables` | List VPC route tables. |
| `aws ec2 describe-security-groups` | List security groups and rules. |
| `aws ec2 create-security-group --group-name web --description "Web access" --vpc-id vpc-0123456789abcdef0` | Create a security group in a VPC. |
| `aws ec2 authorize-security-group-ingress --group-id sg-0123456789abcdef0 --protocol tcp --port 443 --cidr 10.0.0.0/16` | Add an inbound security group rule. |

## Lambda

| Command | Description |
| --- | --- |
| `aws lambda list-functions` | List Lambda functions in the selected region. |
| `aws lambda get-function --function-name my-function` | Retrieve a function's configuration and code location. |
| `aws lambda invoke --function-name my-function response.json` | Invoke a function and save its response. |
| `aws lambda update-function-code --function-name my-function --zip-file fileb://function.zip` | Deploy zipped function code. |
| `aws lambda update-function-configuration --function-name my-function --timeout 30` | Update function runtime settings. |
| `aws lambda publish-version --function-name my-function` | Publish an immutable function version. |

## CloudFormation

| Command | Description |
| --- | --- |
| `aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE UPDATE_COMPLETE` | List successful CloudFormation stacks. |
| `aws cloudformation describe-stacks --stack-name my-stack` | Show stack parameters, outputs, and status. |
| `aws cloudformation deploy --template-file template.yaml --stack-name my-stack --capabilities CAPABILITY_NAMED_IAM` | Create or update a stack from a template. |
| `aws cloudformation validate-template --template-body file://template.yaml` | Validate a local CloudFormation template. |
| `aws cloudformation describe-stack-events --stack-name my-stack` | View recent stack events. |
| `aws cloudformation delete-stack --stack-name my-stack` | Delete a CloudFormation stack. |

## ECS & EKS

| Command | Description |
| --- | --- |
| `aws ecs list-clusters` | List ECS clusters. |
| `aws ecs list-services --cluster production` | List services in an ECS cluster. |
| `aws ecs update-service --cluster production --service api --force-new-deployment` | Force a new ECS service deployment. |
| `aws eks list-clusters` | List EKS clusters. |
| `aws eks describe-cluster --name production` | Retrieve EKS cluster details. |
| `aws eks update-kubeconfig --name production --region us-east-1` | Add an EKS cluster context to kubeconfig. |

## RDS

| Command | Description |
| --- | --- |
| `aws rds describe-db-instances` | List RDS database instances. |
| `aws rds describe-db-clusters` | List Aurora and Multi-AZ DB clusters. |
| `aws rds create-db-snapshot --db-instance-identifier app-db --db-snapshot-identifier app-db-manual` | Create a manual DB instance snapshot. |
| `aws rds restore-db-instance-from-db-snapshot --db-instance-identifier app-db-restored --db-snapshot-identifier app-db-manual` | Restore a DB instance from a snapshot. |
| `aws rds reboot-db-instance --db-instance-identifier app-db` | Reboot an RDS DB instance. |
| `aws rds modify-db-instance --db-instance-identifier app-db --backup-retention-period 7 --apply-immediately` | Modify DB instance settings immediately. |

## CloudWatch & Logs

| Command | Description |
| --- | --- |
| `aws cloudwatch list-metrics --namespace AWS/EC2` | List metrics published in a namespace. |
| `aws cloudwatch get-metric-statistics --namespace AWS/EC2 --metric-name CPUUtilization --dimensions Name=InstanceId,Value=i-0123456789abcdef0 --start-time 2025-01-01T00:00:00Z --end-time 2025-01-01T01:00:00Z --period 300 --statistics Average` | Retrieve aggregated metric data. |
| `aws logs describe-log-groups` | List CloudWatch log groups. |
| `aws logs describe-log-streams --log-group-name /aws/lambda/my-function` | List streams in a log group. |
| `aws logs tail /aws/lambda/my-function --follow` | Follow recent log events from a log group. |
| `aws logs filter-log-events --log-group-name /aws/lambda/my-function --filter-pattern ERROR` | Search log events with a filter pattern. |

## STS

| Command | Description |
| --- | --- |
| `aws sts get-caller-identity` | Show the current AWS account and identity. |
| `aws sts assume-role --role-arn arn:aws:iam::123456789012:role/ReadOnly --role-session-name investigation` | Obtain temporary credentials for a role. |
| `aws sts get-session-token --duration-seconds 3600` | Request temporary session credentials. |
| `aws sts decode-authorization-message --encoded-message ENCODED_MESSAGE` | Decode an EC2 authorization failure message. |
| `aws sts get-access-key-info --access-key-id AKIAIOSFODNN7EXAMPLE` | Identify the account owning an access key. |
| `aws sts assume-role-with-web-identity --role-arn arn:aws:iam::123456789012:role/WebIdentity --role-session-name ci --web-identity-token "$TOKEN"` | Exchange a web identity token for role credentials. |
