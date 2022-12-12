# Create a Managed Spot node group
1. Find instance types matches the criteria
   Selecting instances that match your workload requirements. 
   For the purpose of this workshop we need to first get a group of instances that meet the 4 vCPUs and 16 GB of RAM. 
   ```commandline
   ec2-instance-selector --vcpus 4 --memory 16 --gpus 0 --current-generation -a x86_64 --deny-list '.*[ni].*'
    ```
2. Create Launch Template
```commandline
managed_node_groups = {
     mng_lt = {
      # Node Group configuration
      node_group_name = "mng_lt" # Max 40 characters for node group name

      ami_type               = "AL2_x86_64"  # Available options -> AL2_x86_64, AL2_x86_64_GPU, AL2_ARM_64, CUSTOM
      release_version        = ""            # Enter AMI release version to deploy the latest AMI released by AWS. Used only when you specify ami_type
      capacity_type          = "SPOT"   # ON_DEMAND or SPOT
      instance_types         = instance_types         = ["m4.xlarge", "m5.xlarge", "m5a.xlarge", "m5ad.xlarge", "m5d.xlarge", "m6a.xlarge", "t2.xlarge", "t3.xlarge", "t3a.xlarge"]
      format_mount_nvme_disk = true          # format and mount NVMe disks ; default to false

      # Launch template configuration
      create_launch_template = true              # false will use the default launch template
      launch_template_os     = "amazonlinux2eks" # amazonlinux2eks or bottlerocket

      enable_monitoring = true
      eni_delete        = true
      public_ip         = false # Use this to enable public IP for EC2 instances; only for public subnets used in launch templates

      http_endpoint               = "enabled"
      http_tokens                 = "optional"
      http_put_response_hop_limit = 3

      # pre_userdata can be used in both cases where you provide custom_ami_id or ami_type
      pre_userdata = <<-EOT
        yum install -y amazon-ssm-agent
        systemctl enable amazon-ssm-agent && systemctl start amazon-ssm-agent
      EOT

      # Taints can be applied through EKS API or through Bootstrap script using kubelet_extra_args
      # e.g., k8s_taints = [{key= "spot", value="true", "effect"="NO_SCHEDULE"}]
      k8s_taints = []

      # Node Labels can be applied through EKS API or through Bootstrap script using kubelet_extra_args
      k8s_labels = {
        Environment = "preprod"
        Zone        = "dev"
        Runtime     = "docker"
        Node_Type   = "Spot"
      }

      # Node Group scaling configuration
      desired_size = 2
      max_size     = 2
      min_size     = 2

      block_device_mappings = [
        {
          device_name = "/dev/xvda"
          volume_type = "gp3"
          volume_size = 100
        }
      ]

      # Node Group network configuration
      subnet_type = "private" # public or private - Default uses the private subnets used in control plane if you don't pass the "subnet_ids"
      subnet_ids  = []        # Defaults to private subnet-ids used by EKS Control plane. Define your private/public subnets list with comma separated subnet_ids  = ['subnet1','subnet2','subnet3']

      additional_iam_policies = [] # Attach additional IAM policies to the IAM role attached to this worker group

      # SSH ACCESS Optional - Recommended to use SSM Session manager
      remote_access         = false
      ec2_ssh_key           = ""
      ssh_security_group_id = ""

      additional_tags = {
        ExtraTag    = "m5x-on-demand"
        Name        = "m5x-on-demand"
        subnet_type = "private"
      }
    }

```
3. Apply updates terraform code
```commandline
terraform plan
terraform apply
```