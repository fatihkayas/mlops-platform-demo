# 🚀 Production-Grade MLOps Platform

![Build](https://img.shields.io/badge/build-passing-brightgreen) ![Terraform](https://img.shields.io/badge/IaC-Terraform-7B42BC) ![AWS](https://img.shields.io/badge/cloud-AWS-FF9900) ![Security](https://img.shields.io/badge/auth-OIDC%20(no%20keys)-00C7B7) ![License](https://img.shields.io/badge/license-MIT-blue)

> End-to-end MLOps platform built on AWS SageMaker, GitHub Actions, and Terraform.  
> Designed to production standards: zero long-lived credentials, drift monitoring, IaC security scanning, and automated rollback.

👉 [View full roadmap →](./ROADMAP.md)

---

## 📐 Architecture Overview

```
GitHub Push
    │
    ▼
GitHub Actions (OIDC → AWS Role)
    │
    ▼
SageMaker Pipeline
    ├── Data Quality Validation  (Great Expectations)
    ├── Feature Engineering      (SageMaker Feature Store)
    ├── Model Training           (HPO via SageMaker Tuner)
    ├── Bias Detection           (SageMaker Clarify)
    └── Conditional Registration (Model Registry — if accuracy > threshold)
         │
         ▼
    Staging Endpoint
         │
    Manual Approval
         │
         ▼
    Production Endpoint
         │
    SageMaker Model Monitor
    ├── Data Drift Detection
    └── SNS Alert → CloudWatch Dashboard
```

---

## ✨ Key Design Decisions (vs standard AWS blog approach)

| Topic | Standard Approach | This Project |
|-------|-------------------|--------------|
| AWS Auth | IAM User + Access Key | **GitHub OIDC** — zero long-lived credentials |
| Data Quality | None | **Great Expectations** validation before training |
| Feature Management | Ad-hoc scripts | **SageMaker Feature Store** (offline + online) |
| Bias Detection | None | **SageMaker Clarify** integrated in pipeline |
| Model Drift | None | **SageMaker Model Monitor** + SNS alerting |
| IaC Security | None | **tfsec + checkov** in CI pipeline |
| Terraform State | Local | **S3 + DynamoDB locking** (remote, team-safe) |
| Deployment Safety | None | **Automated rollback** on failed health check |
| CI for Terraform | Manual apply | **Plan on PR, apply on merge** |

---

## 🗂️ Project Structure

```
├── .github/
│   └── workflows/
│       ├── build.yml
│       ├── deploy.yml
│       └── shared/
│
├── training/
│   └── train.py
│
├── scripts/
│   ├── preprocess.py
│   └── evaluate.py
│
├── pipeline/
│   └── pipeline.py
│
├── terraform/
│   ├── modules/
│   │   ├── s3/
│   │   ├── iam/
│   │   ├── lambda/
│   │   ├── ecr/
│   │   └── eventbridge/
│   └── environments/
│       ├── dev/
│       ├── staging/
│       └── prod/
│
└── monitoring/
    └── model_monitor_config.py
```

---

## 🔐 Security Architecture

```
GitHub Actions Runner
        │
        │  OIDC Token (JWT)
        ▼
AWS STS AssumeRoleWithWebIdentity
        │
        ▼
  Scoped IAM Role (least privilege)
        │
        ▼
  SageMaker / S3 / ECR / Lambda
```

No IAM user. No access keys. No long-lived credentials stored anywhere.  
IaC is scanned on every pull request with `tfsec` and `checkov` before any infrastructure change is applied.

---

## 📄 Architecture Decision Records

| ADR | Decision | Status |
|-----|----------|--------|
| ADR-001 | GitHub OIDC over IAM User | Accepted |
| ADR-002 | SageMaker Feature Store for feature reuse | Accepted |
| ADR-003 | Terraform remote state with DynamoDB locking | Accepted |
| ADR-004 | Conditional model registration (accuracy gate) | Accepted |
| ADR-005 | tfsec + checkov in CI (shift-left security) | Accepted |

---

## 🛠️ Setup Instructions

### Prerequisites
- AWS account with SageMaker domain
- GitHub repository
- AWS CLI configured
- Terraform >= 1.5

### 1. Configure GitHub OIDC

```bash
cd terraform/environments/dev
terraform init
terraform plan
terraform apply
```

### 2. Set GitHub Repository Secrets

```
AWS_ROLE_ARN       → ARN of the OIDC role (from Terraform output)
AWS_REGION         → e.g. eu-central-1
SAGEMAKER_PROJECT  → your SageMaker project name
```

### 3. Run the Pipeline

Push to `main` — GitHub Actions triggers the full build and deploy workflow automatically.

---

## 👤 Author

Built as a production-grade portfolio project demonstrating senior MLOps engineering practices.  
Inspired by the [AWS MLOps blog](https://aws.amazon.com/blogs/machine-learning/) — extended with enterprise patterns not covered there.