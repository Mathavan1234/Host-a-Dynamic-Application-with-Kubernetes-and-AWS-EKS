![Alt text](/Reference_Architecture_Diagram.jpg)
# Host a Dynamic Application with Kubernetes and AWS EKS

## Overview
This project demonstrates how to deploy a dynamic web application using **Kubernetes** on **AWS EKS**. It covers infrastructure setup, containerization, database migration, and application deployment using AWS services.

## Tech Stack
- **AWS Services:** EKS, EC2, RDS, S3, IAM, Route 53, NAT Gateway, ALB, NLB, CloudFormation
- **Kubernetes:** Deployments, Services, Secrets, Namespaces, Pods
- **Docker & ECR:** Containerization and Image Repository
- **Helm:** Secret management in AWS Secret Manager

## Project Architecture
The project follows a **3-tier VPC architecture**:
1. **Public Subnet**: NAT Gateway, ALB, Bastion Host
2. **Private Subnet**: Web Servers (EKS Worker Nodes)
3. **Private Subnet**: RDS Database

All resources are replicated across **two Availability Zones** for **high availability** and **fault tolerance**.

## Deployment Steps

### 1️⃣ **Setup SSH Key Pair**
- Generate an SSH key pair to authenticate with GitHub and clone the repository.
- Add the **public key** to GitHub.

### 2️⃣ **Setup AWS Infrastructure**
- Create a **Custom VPC** with **enabled DNS hostnames**.
- Setup **Internet Gateway** and attach it to the VPC.
- Create **Public & Private Subnets**.
- Configure **Route Tables** for public and private subnets.

### 3️⃣ **Configure Networking & Security**
- **NAT Gateway**: Allow private subnets to access the internet.
- **Security Groups**: Define firewall rules for EC2, RDS, and EKS components.
- **EC2 Instance Connect Endpoint**: Enable SSH access without managing keys.

### 4️⃣ **Setup RDS Database**
- Create **RDS Instance** and **subnet groups**.
- Store **database credentials** securely in AWS Secret Manager.

### 5️⃣ **Docker Image & ECR Repository**
- Create a **Dockerfile** for the application.
- Build and push the image to **Amazon ECR**.

### 6️⃣ **Data Migration to RDS**
- Upload SQL data script to **S3 Bucket**.
- Assign **IAM Role** to EC2 for accessing S3.
- Run migration script from EC2.

### 7️⃣ **Deploy Application on AWS EKS**
- **Create EKS Cluster** and **IAM Role** for Kubernetes.
- Setup **Worker Nodes (EC2 instances)** for hosting containers.
- Define **Kubernetes Manifest Files**:
  - **Secret Provider Class**: Mount AWS Secrets Manager to EKS.
  - **Deployment YAML**: Manage application scaling.
  - **Service YAML**: Expose app using Network Load Balancer.

### 8️⃣ **Setup IAM OIDC & Service Accounts**
- Associate **IAM OIDC Identity Provider** with EKS.
- Create **IAM Service Account** via CloudFormation.

### 9️⃣ **Configure Load Balancer & DNS**
- Apply **Service YAML** to automatically create **NLB & Target Group**.
- Set up **Route 53 A Record** for domain mapping.

## Final Deployment Outcome 🎉
🚀 The application is now hosted on **AWS EKS** and accessible via the configured **NLB and Route 53 domain**.
 
📌 Medium: [Aricle:](https://medium.com/@smaddy799/host-a-dynamic-application-with-kubernetes-and-aws-eks-a94f0dc716e3)

