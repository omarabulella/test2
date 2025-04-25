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
