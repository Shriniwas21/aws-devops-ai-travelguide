# DevOps & AI Project – TravelGuideAI on AWS

## 📌 Overview
Hands-on project from Coursera's "DevOps and AI on AWS" specialization. This project involves deploying a Flask-based AI travel app using cloud-native DevOps practices.
📘 Note: This repository was originally created in 2025 and updated in 2026 while revisiting the AWS DevOps & AI specialization to refresh concepts and improve documentation.

## 🛠️ Technologies
- **Cloud Services**: Amazon EC2, S3, DynamoDB, CloudWatch, X-Ray, Systems Manager, OpenSearch Serverless
- **AI/ML**: Amazon Bedrock (Titan G1 & Embedding V2), Knowledge Base (RAG)
- **DevOps**: AWS CDK, CodePipeline, CodeBuild, GitHub, CI/CD, Infrastructure-as-Code
- **Programming**: Python, Flask, PyLint, unittest, coverage
- **Deployment**: systemd, NGINX, userdata scripts

## 🔍 Labs

| Lab | Title |
|-----|-------------------------------|
| 1 | Setup Code Quality & Unit Testing |
| 2 | Bedrock AI Integration & EC2 Deployment |
| 3 | Setup CI/CD Pipeline |
| 4 | Deploy Infrastructure with CDK |
| 5 | Monitor with CloudWatch Anomaly Detection |
| 6 | Use Systems Manager for Diagnostics |
| 7 | Add AIOps with X-Ray |

## 📸 Screenshots
Each lab folder contains relevant screenshots and test outputs to demonstrate progress.

## 🔍 Labs Progress

| Lab | Title | Status | Key Tasks |
|-----|-------|--------|-----------|
| 1 | Code Quality & Unit Testing | ✅ Completed | Flask app run, PyLint, test coverage |
| 2 | Bedrock AI + EC2 Deploy | ✅ Completed | Bedrock integration, KB config, EC2 deployment |
| 3 | Setup CI/CD Pipeline | ✅ Completed | CodeBuild + CodeDeploy integration, pipeline triggered via `Release change` |
| 4 | Deploy Infra with CDK | ✅ Completed | CDK app, CloudFormation stack, EC2 + IAM provisioning |
| 5 | CloudWatch Anomaly Detection | ✅ Completed | Anomaly detector + alarm, CLI metric analysis, custom metrics |
| 6 | Systems Manager Diagnostics | 🔜 | |
| 7 | AIOps with X-Ray | 🔜 | |

## 📁 Labs Directory

- [Lab 1: Setup Code Quality & Unit Testing](./lab1-setup-code-quality/)
- [Lab 2: Bedrock AI Integration & EC2 Deployment](./lab2-deploy-base-app/)
- [Lab 3: Setup CI/CD Pipeline](./lab3-setup-cicd/)
- [Lab 4: Deploy Infrastructure with CDK](./lab4-cdk-infra-deploy/)
- [Lab 5: Monitor with CloudWatch Anomaly Detection](./lab5-cloudwatch-anomaly/)

## 🧪 Next Steps
- Continue Labs 6–7 to complete end-to-end DevOps pipeline
- (Optional) Extend project with Docker, GitHub Actions CI/CD
- (Optional) Re-deploy on AWS Free Tier for public showcase
