# Complete DevOps Pipeline Implementation

## 📚 Project Overview
This project simulates a real-world DevOps workflow by designing, automating, and deploying a containerized Python web application. The project demonstrates the full DevOps lifecycle—covering version control, infrastructure provisioning with Terraform and Ansible, containerization using Docker, orchestration on Kubernetes via AWS EKS, automated CI/CD with Jenkins, monitoring with Prometheus and Grafana, and secure secrets management. The final output includes working infrastructure, pipeline execution, and comprehensive documentation.

## 🛠 Technologies Used
- **AWS (EKS, EC2, S3, ECR)**
- **Terraform** (Infrastructure Provisioning)
- **Ansible** (Server Configuration)
- **Docker** (Containerization)
- **Kubernetes** (Orchestration)
- **Jenkins** (CI/CD Automation)
- **Prometheus and Grafana** (Monitoring)
- **GitHub** (Version Control)

## 📋 Prerequisites

Before starting, ensure you have the following tools installed:
- **Terraform**: To provision infrastructure on AWS (EKS, EC2, S3).
- **Ansible**: For automating the Jenkins setup.
- **AWS CLI**: For managing AWS resources from the command line.
- **kubectl**: To interact with the Kubernetes cluster.
  

## How to Set Up the Project

### Step 1: Clone the Repository
Clone the repository to your local machine:

```bash
git clone https://github.com/omarabulella/Complete-DevOps-Pipeline-Implementation.git
cd Complete-DevOps-Pipeline-Implementation
```

## Step 2: Set Up AWS Credentials
Ensure your AWS credentials are configured to allow Terraform and AWS CLI to provision resources.
```bash
aws configure
```
## Step 3: Provision Infrastructure with Terraform

This project uses **Terraform** to provision the necessary infrastructure on AWS. The infrastructure includes:

- An **EKS (Elastic Kubernetes Service)** cluster with two nodes.
- A **CI/CD EC2 instance** (Virtual Machine) for Jenkins.
- An **S3 bucket** to store Terraform state files.

### 3.1: Set up Terraform Variables

Before running the Terraform script, ensure that you have set the required values for the variables. These values are used for AWS resource creation (like AWS region, instance types, and other configurations).

You can either define the variable values in a `terraform.tfvars` file or manually input them when prompted.

**Example of a `terraform.tfvars` file:**

```hcl
# terraform.tfvars
region="us-east-2"
ec2_instance_type="t2.micro"
Eks_cluster_name="my-eks-cluster"
vpc_cidr="10.0.0.0/16"
ssh_key_name = "my-ssh-key"
ssh_key_path = "~/.ssh/my-key.pem"
s3_bucket_name = "my-terraform-state-bucket-konecta"
ami_id = "ami-04f167a56786e4b09"

```
### 3.2:  Initialize Terraform
```bash
terraform init
```
This command initializes Terraform and installs the necessary provider plugins.
### 3.3:  Apply Terraform Configuration
```bash
terraform apply
```
Terraform will prompt you to confirm the infrastructure creation. Type yes to proceed.
### 3.4: Ansible Playbook Trigger
Once the EC2 instance is provisioned, the Terraform script will automatically trigger a Bash script that checks the availability of the VM and then runs the Ansible playbook to configure Jenkins on the VM. This ensures that the Jenkins setup is automated without any manual intervention.

The Bash script (located in /scripts/config_cicd.sh) will:

Check if the EC2 instance is up and running.

Automatically apply the Ansible playbook to install and configure Jenkins.

You don't need to manually trigger this step—Terraform will handle it automatically after the infrastructure is provisioned.
## Step 4: SSH into the EC2 Instance and Deploy Kubernetes Resources

After successfully provisioning the infrastructure, I SSH into the **CI/CD EC2 instance** that was created using Terraform. This VM is configured to host **Jenkins** for automating the CI/CD pipeline. Here’s a breakdown of what I did next to set up and deploy the app.
### 4.1: SSH into the EC2 Instance

To begin configuring Jenkins and deploying my app to the Kubernetes cluster, I first needed to SSH into the EC2 instance. Here’s the command I used to access the instance:

```bash
ssh -i /path/to/your/key.pem ec2-user@<EC2_PUBLIC_IP>
```
## Step 5: Set Up Jenkins for CI/CD
Once you’ve SSH'd into the EC2 instance and ensured Jenkins is installed, follow these steps to set up the Jenkins pipeline:
### 1. Install Required Jenkins Plugins:
### 2. Add Required  Credentials to Jenkins: Store the following credentials in Jenkins:
*REGION: 
* cluster-name: 
* image-name: 
* AWS_ACCOUNT_ID: 
* ECR_REPO:
### 3. Create a Multibranch Pipeline:
