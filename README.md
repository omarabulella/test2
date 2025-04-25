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

aws_access_key = "YOUR_AWS_ACCESS_KEY"
aws_secret_key = "YOUR_AWS_SECRET_KEY"
region         = "us-east-1"
eks_node_type  = "t2.medium"
eks_node_count = 2
instance_type  = "t2.micro"
key_name       = "your-key-pair-name"

```
