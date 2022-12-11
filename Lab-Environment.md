# Configure AWS Lab Environment
For this workshop you will need an IDE environment for running AWS CLI commands and terraform commands. we can cloud9 to avoid any workstation OS related confusions
## Cloud 9
Use the CloudFormation stack in below to create Cloud9, which will include:
- An Amazon Virtual Private Cloud (Amazon VPC) with subnets in two Availability Zones
- An AWS Cloud9 environment
- Supporting IAM policies and roles
- Supporting security groups 
  
Setup with Cloudformation - [instructions here](https://ec2spotworkshops.com/ec2-auto-scaling-with-multiple-instance-types-and-purchase-options/launch_cloudformation.html)

you can access cloud9 in AWS console [here](https://console.aws.amazon.com/cloud9/)

## Prerequisite Tools
First, We have to install following tools for the lab in Cloud9
1. aws cli
   - Follow installation steps [here](https://ec2spotworkshops.com/ec2-auto-scaling-with-multiple-instance-types-and-purchase-options/setup_cli.html)
2. kubectl
```commandline
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-\$basearch
enabled=1
gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
sudo yum install -y kubectl
```  
Ref: [here](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

3. terraform (Already installed in cloud9)
- Verify the terraform version
```commandline
terraform -version
```
Output:
```commandline
Terraform v1.3.6
on linux_amd64
```

## Cloud9 IAM Role
1. Attach an Admin role to cloud9 - Follow instructions [here](https://ec2spotworkshops.com/using_ec2_spot_instances_with_eks/010_prerequisites/attach_workspaceiam.html)
2. Update IAM settings in Cloud9 - Follow instructions [here](https://ec2spotworkshops.com/using_ec2_spot_instances_with_eks/010_prerequisites/update_workspaceiam.html)