# AWS DevSecOps Project – ECS Fargate with GitHub Actions (OIDC)

## 📌 Project Overview

This project demonstrates a **real-world AWS DevSecOps implementation** using **Amazon ECS with AWS Fargate** and **GitHub Actions**.

The focus of this project is:
- Secure CI/CD
- Containerized application deployment
- Zero long-lived AWS credentials using **OIDC**
- Clear separation of infrastructure and application delivery

---

## 🧱 Architecture Summary

- **Container Orchestrator:** Amazon ECS  
- **Compute Engine:** AWS Fargate  
- **Container Registry:** Amazon ECR  
- **Load Balancer:** Application Load Balancer (ALB)  
- **CI/CD:** GitHub Actions  
- **Authentication:** IAM OIDC (no AWS access keys)  
- **Infrastructure as Code:** Terraform  

---

## 🚀 What is AWS Fargate?

**AWS Fargate is a serverless compute engine for containers.**

With Fargate:
- You do **not** manage EC2 instances
- You do **not** patch or scale servers
- You only define:
  - Container image
  - CPU and memory
  - Networking rules

AWS automatically handles:
- Server provisioning
- Scaling
- OS and security patching

👉 **In simple terms:**  
**Fargate runs your containers without you managing servers.**

---

## 📦 What is Amazon ECS?

**Amazon ECS (Elastic Container Service)** is AWS’s **native container orchestration service**.

ECS is responsible for:
- Scheduling containers
- Restarting failed tasks
- Integrating with AWS services like ALB, IAM, and CloudWatch

ECS can run containers using:
- **EC2** (you manage servers)
- **Fargate** (AWS manages servers)

👉 **In this project:**  
We use **ECS + Fargate**, meaning AWS manages both the orchestration and the compute layer.

---

## ☸️ What is Amazon EKS?

**Amazon EKS (Elastic Kubernetes Service)** is AWS’s managed **Kubernetes** offering.

With EKS:
- AWS manages the Kubernetes control plane
- You still work with Kubernetes concepts:
  - Pods
  - Deployments
  - Services
  - `kubectl`
- Worker nodes can run on:
  - EC2
  - Fargate

👉 **EKS is Kubernetes on AWS**, suitable for teams already standardized on Kubernetes.

---

## 🔍 ECS vs EKS – Key Differences

| Feature | ECS (This Project) | EKS |
|------|------------------|-----|
| Orchestrator | AWS-native | Kubernetes |
| Complexity | Low | High |
| Kubernetes required | ❌ No | ✅ Yes |
| YAML manifests | ❌ No | ✅ Yes |
| Control plane | Fully AWS-managed | Kubernetes API |
| Operational overhead | Minimal | Higher |
| Best use case | AWS-native workloads | Kubernetes portability |

---

## 🔗 Where Does Fargate Fit In?

Fargate can be used with **both ECS and EKS**:

| Platform | Supports Fargate |
|-------|----------------|
| ECS | ✅ Yes |
| EKS | ✅ Yes |

In this project:
- **ECS + Fargate** was chosen for simplicity
- Focus is on **DevSecOps fundamentals**, not Kubernetes operations

---

## 🔐 DevSecOps Highlights

This project demonstrates several key DevSecOps best practices:

- No AWS access keys stored in GitHub
- Authentication via **GitHub Actions OIDC**
- Short-lived STS credentials
- Infrastructure managed separately from CI/CD
- Immutable container deployments via ECR
- Controlled network access using security groups

---

## 🔄 CI/CD Flow (High Level)

1. Developer pushes code to GitHub
2. GitHub Actions pipeline starts
3. GitHub authenticates to AWS using OIDC
4. Docker image is built
5. Image is pushed to Amazon ECR
6. ECS service is triggered for a rolling deployment
7. Application is served via ALB

---

## 🎯 Why ECS + Fargate Was Chosen

ECS with Fargate was selected to:
- Reduce operational complexity
- Avoid Kubernetes overhead
- Focus on secure CI/CD and AWS-native DevSecOps practices

The same CI/CD and security concepts used here **apply directly to EKS**.

---



## ✅ Key Takeaway

**ECS manages containers, Fargate runs them without servers, and EKS is Kubernetes on AWS.**
