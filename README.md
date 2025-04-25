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
  
## 📁 Project Structure
graduation-project/
├── application/ 
│ ├── static/ 
│ ├── templates/ 
│ ├── tests/ 
│ ├── Dockerfile 
│ ├── hello.py 
│ └── requirements.txt 
├── CICD/ 
│ └── Jenkinsfile 
├── infra/ 
│ ├── ansible/ 
│ │ ├── inventory.ini 
│ │ └── playbook.yml 
│ ├── scripts/ 
│ │ └── config_cicd.sh 
│ ├── terraform/ 
│ │ ├── backend.tf  
│ │ ├── main.tf  
│ │ ├── outputs.tf
│ │ └── variables.tf  
│ ├── k8s/ 
│ | ├── app-deployment.yml 
│ | ├── configmap.yml 
│ | ├── namespace.yml 
│ | └── service.yml
