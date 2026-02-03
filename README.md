# AWS EC2 Provisioning with Terraform:

This project demonstrates the core concepts of AWS and Terraform by provisioning an EC2 instance manually and using Infrastructure as Code (IaC) with Terraform. The objective is to show proficiency in cloud computing, Terraform basics, and reproducible infrastructure deployment.

# AWS core concepts and Terraform :-

This project demonstrates the core concepts of AWS and Terraform by provisioning an EC2 instance manually and using Infrastructure as Code (IaC) with Terraform. 

# Key objectives achieved:
- Learned AWS core concepts such as EC2 instances, AMIs, instance types, security groups, and key pairs.
- Learned Terraform basics: providers, resources, variables, outputs, and automation of cloud infrastructure.
- Practiced launching EC2 manually and provisioning it automatically using Terraform.

# Launching EC2 Manually

Steps:

Login to your AWS Management Console.
Navigate to EC2 → Instances → Launch Instance.
Choose an Amazon Machine Image (AMI) (e.g., Ubuntu 22.04 LTS).
Select an Instance Type (e.g., t3.micro).
Configure instance details (default VPC, subnet, etc.).
Add storage if required.
Configure security group:
Allow SSH (port 22) from your IP
Allow HTTP (port 80) if required
Review and Launch using an existing or new key pair.

EC2 instance is now running and accessible via SSH.

**Provisioning EC2 with Terraform**

Project-Structure : 
terraform-ec2/
├── main.tf        # Provider and resource definitions
├── variables.tf   # Input variables
├── outputs.tf     # Outputs for easy access
└── terraform.tfvars # Variable values

**1. Terraform Configuration(ec2.tf) :-** 

ubuntu@ip-172-31-35-188:~/terraform-for-task2$ cat ec2.tf


resource "aws_instance" "ec2_for_task2" {
  ami           = "ami-0f5ee92e2d63afc18"
  instance_type = "t3.micro"
  key_name      = "terra-server-key-task-2"

  tags = {
    Name = "terraform-ec2-task2"
  }
}

# 2. Terraform Initialization and Execution :-

**2.A terraform init :-**

ubuntu@ip-172-31-35-188:~/terraform-for-task2$ terraform init
Initializing the backend...
Initializing provider plugins...
- Reusing previous version of hashicorp/local from the dependency lock file
- Reusing previous version of hashicorp/aws from the dependency lock file
- Using previously-installed hashicorp/local v2.6.2
- Using previously-installed hashicorp/aws v6.30.0

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

2.B terraform validate :- 

ubuntu@ip-172-31-35-188:~/terraform-for-task2$ terraform validate
Success! The configuration is valid.

# 2.C terraform plan :-

ubuntu@ip-172-31-35-188:~/terraform-for-task2$ terraform plan
local_file.my_file: Refreshing state... [id=3506da7345dd40ff034ad248617e0b74fd931106]
aws_s3_bucket.my-bucket: Refreshing state... [id=devansh-terraform-learning]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the follow
symbols:
  + create

Terraform will perform the following actions:

  aws_instance.ec2_simple will be created
  + resource "aws_instance" "ec2_simple" {
      + ami                                  = "ami-0f30a9c3a48f3fa79"
      + arn                                  = (known after apply)
      + associate_public_ip_address          = (known after apply)
      + availability_zone                    = (known after apply)
      + disable_api_stop                     = (known after apply)
      + disable_api_termination              = (known after apply)
      + ebs_optimized                        = (known after apply)
      + enable_primary_ipv6                  = (known after apply)
      + force_destroy                        = false
      + get_password_data                    = false
      + host_id                              = (known after apply)
      + host_resource_group_arn              = (known after apply)
      + iam_instance_profile                 = (known after apply)
      + id                                   = (known after apply)
      + instance_initiated_shutdown_behavior = (known after apply)
      + instance_lifecycle                   = (known after apply)
      + instance_state                       = (known after apply)
      + instance_type                        = "t3.micro"
      + ipv6_address_count                   = (known after apply)
      + ipv6_addresses                       = (known after apply)
      + key_name                             = (known after apply)
      + monitoring                           = (known after apply)
      + outpost_arn                          = (known after apply)
      + password_data                        = (known after apply)
      + placement_group                      = (known after apply)
      + placement_group_id                   = (known after apply)
      + placement_partition_number           = (known after apply)
      + primary_network_interface_id         = (known after apply)
      + private_dns                          = (known after apply)
      + private_ip                           = (known after apply)
      + public_dns                           = (known after apply)
      + public_ip                            = (known after apply)
      + region                               = "us-east-2"
      + secondary_private_ips                = (known after apply)
      + security_groups                      = (known after apply)
      + source_dest_check                    = true
      + spot_instance_request_id             = (known after apply)
      + subnet_id                            = (known after apply)
      + tags_all                             = (known after apply)
      + tenancy                              = (known after apply)
      + user_data_base64                     = (known after apply)
      + user_data_replace_on_change          = false
      + vpc_security_group_ids               = (known after apply)

      + capacity_reservation_specification (known after apply)

      + cpu_options (known after apply)

      + ebs_block_device (known after apply)

      + enclave_options (known after apply)

      + ephemeral_block_device (known after apply)

      + instance_market_options (known after apply)

      + maintenance_options (known after apply)

      + metadata_options (known after apply)

      + network_interface (known after apply)

      + primary_network_interface (known after apply)

      + private_dns_name_options (known after apply)

      + root_block_device (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run
"terraform apply" now.


**2.D terraform apply :-**

ubuntu@ip-172-31-35-188:~/terraform-for-task2$ terraform apply
local_file.my_file: Refreshing state... [id=3506da7345dd40ff034ad248617e0b74fd931106]
aws_s3_bucket.my-bucket: Refreshing state... [id=devansh-terraform-learning]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the follow
symbols:
  + create

Terraform will perform the following actions:

  **aws_instance.ec2_simple will be created**
  + resource "aws_instance" "ec2_simple" {
      + ami                                  = "ami-0f30a9c3a48f3fa79"
      + arn                                  = (known after apply)
      + associate_public_ip_address          = (known after apply)
      + availability_zone                    = (known after apply)
      + disable_api_stop                     = (known after apply)
      + disable_api_termination              = (known after apply)
      + ebs_optimized                        = (known after apply)
      + enable_primary_ipv6                  = (known after apply)
      + force_destroy                        = false
      + get_password_data                    = false
      + host_id                              = (known after apply)
      + host_resource_group_arn              = (known after apply)
      + iam_instance_profile                 = (known after apply)
      + id                                   = (known after apply)
      + instance_initiated_shutdown_behavior = (known after apply)
      + instance_lifecycle                   = (known after apply)
      + instance_state                       = (known after apply)
      + instance_type                        = "t3.micro"
      + ipv6_address_count                   = (known after apply)
      + ipv6_addresses                       = (known after apply)
      + key_name                             = (known after apply)
      + monitoring                           = (known after apply)
      + outpost_arn                          = (known after apply)
      + password_data                        = (known after apply)
      + placement_group                      = (known after apply)
      + placement_group_id                   = (known after apply)
      + placement_partition_number           = (known after apply)
      + primary_network_interface_id         = (known after apply)
      + private_dns                          = (known after apply)
      + private_ip                           = (known after apply)
      + public_dns                           = (known after apply)
      + public_ip                            = (known after apply)
      + region                               = "us-east-2"
      + secondary_private_ips                = (known after apply)
      + security_groups                      = (known after apply)
      + source_dest_check                    = true
      + spot_instance_request_id             = (known after apply)
      + subnet_id                            = (known after apply)
      + tags_all                             = (known after apply)
      + tenancy                              = (known after apply)
      + user_data_base64                     = (known after apply)
      + user_data_replace_on_change          = false
      + vpc_security_group_ids               = (known after apply)

      + capacity_reservation_specification (known after apply)

      + cpu_options (known after apply)

      + ebs_block_device (known after apply)

      + enclave_options (known after apply)

      + ephemeral_block_device (known after apply)

      + instance_market_options (known after apply)

      + maintenance_options (known after apply)

      + metadata_options (known after apply)

      + network_interface (known after apply)

      + primary_network_interface (known after apply)

      + private_dns_name_options (known after apply)

      + root_block_device (known after apply)
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

aws_instance.ec2_simple: Creating...
aws_instance.ec2_simple: Still creating... [00m10s elapsed]
aws_instance.ec2_simple: Creation complete after 14s [id=i-088fca5df649c5a74]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.


# CONCLUSION :

This project covers both manual and automated provisioning of AWS EC2 instances. By using Terraform, we achieve:
Reproducibility: Same infrastructure can be deployed multiple times
Automation: Eliminates manual configuration
Version Control: Infrastructure can be managed like code

Skills Demonstrated:
AWS EC2 launch
Security group configuration
Terraform basics: provider, resource, variable, output
Infrastructure as Code (IaC) principles.