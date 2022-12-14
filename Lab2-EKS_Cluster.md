# Build Amazon EKS with Terraform
In this lab, we will deploy 
- new VPC
- private EKS cluster with public and private subnets
- one managed node group that will be placed in the private subnets

also following add-ons
- AWS Load Balancer Controller
- Cluster Autoscaler
- CoreDNS
- kube-proxy
- Metrics Server
- vpc-cni

## Steps:
1. Clone the repo
```commandline
git clone https://github.com/aws-ia/terraform-aws-eks-blueprints.git
cd terraform-aws-eks-blueprints/examples/eks-cluster-with-new-vpc/
```
2. Initialize the working directory (Terraform INIT)
```commandline
terraform init
```
Note: This step will copy modules to working directory. New directory inside working directory `.terraform`
3. Verify the resources that will be created by this execution (Terraform PLAN):
```commandline
terraform plan
```
Note: This command does not actually carry out the proposed changes You can use this command to check whether the proposed changes match what you expected before you apply the changes or share your changes with your team for broader review.
4. Deploying AWS resources into the account (Terraform APPLY)
   - Create VPC 
     ```commandline
     terraform apply -target="module.vpc"
     ```
   - Create EKS
     ```commandline
     terraform apply -target="module.eks_blueprints"
     ```
   - Deploy the add-ons
     ```commandline
     terraform apply
     ```
Note: Terraform State file will be stored locally in the working directory `terraform.tfstate`
5. Run output of `configure_kubectl` from Terraform outputs
   ```commandline
   aws eks --region us-west-2 update-kubeconfig --name eks-cluster-with-new-vpc
   ```
Note: This step will add EKS cluster context into your kube config file (/home/ec2-user/.kube/config)
6. Validate EKS cluster resources
   - List nodes
    ```commandline
    kubectl get nodes
    ``` 
   - List pods
    ````commandline
    kubectl get pods -n kube-system
    ````
Note: `-n` is the key to choose a specific namespace inside kubernetes cluster
