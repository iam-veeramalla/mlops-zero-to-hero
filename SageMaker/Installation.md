# Install SageMaker using AWS CLI

### Create Policy

# Create IAM Trust Policy for SageMaker

Use the following command to create a file named `trust-policy.json` with the required trust relationship for SageMaker.

```
cat > trust-policy.json << 'EOF'
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "sagemaker.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
EOF
```

### Create an execution role and attach AmazonSageMakerFullAccess policy

```
aws iam create-role --role-name sagemaker-admin --assume-role-policy-document file://trust-policy.json
aws iam attach-role-policy --role-name sagemaker-admin --policy-arn arn:aws:iam::aws:policy/AmazonSageMakerFullAccess
```

### Get the VPC and Subnet details (Networking)

In the second command, replace <default-vpc-id> with your VPC ID -> (Output of first command).

```
aws --region ap-south-1 ec2 describe-vpcs --filters Name=isDefault,Values=true --query "Vpcs[0].VpcId" --output text
aws --region ap-south-1 ec2 describe-subnets --filters Name=vpc-id,Values=<default-vpc-id> --query "Subnets[*].SubnetId" --output json
```

### Create SageMaker domain 

Replace "default-vpc-id", "subnet-id>", "account-number" and "image-arn".

You can find the <image-arn> for your region below.

`https://docs.aws.amazon.com/sagemaker/latest/dg/studio-jl.html#studio-jl-set`

```
aws --region ap-south-1 sagemaker create-domain \
  --domain-name demo-mlops \
  --vpc-id <default-vpc-id> \
  --subnet-ids <subnet-ids> \
  --auth-mode IAM \
  --default-user-settings "ExecutionRole=arn:aws:iam::<account-number>:role/sagemaker-admin, \
  JupyterServerAppSettings={DefaultResourceSpec={InstanceType=system, \
  SageMakerImageArn=<image-arn>}}"
```
