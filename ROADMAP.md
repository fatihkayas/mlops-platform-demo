# 🗺️ MLOps Platform — Roadmap

> Her phase tamamlandığında `🔜` → `✅` olarak güncelle.

---

## 📊 Progress Overview

| Phase | Topic | Duration | Status |
|-------|-------|----------|--------|
| 01 | Architecture & Design | 2d | ✅ Done |
| 02 | Core ML Pipeline | 3d | ⚡ Active |
| 03 | SageMaker Pipeline + Feature Store | 3d | 🔜 |
| 04 | CI/CD — GitHub Actions + OIDC | 2d | 🔜 |
| 05 | Infrastructure as Code — Terraform | 3d | 🔜 |
| 06 | Security Hardening | 2d | 🔜 |
| 07 | Monitoring & Model Observability | 2d | 🔜 |
| 08 | Portfolio Polish & Demo | 2d | 🔜 |
| | **Total** | **~18d** | |

---

## ✅ Phase 01 — Architecture & Design `done` · 2d

**Stack:** Draw.io / Excalidraw · ADR · C4 Model · Confluence

| Status | Task | Level |
|--------|------|-------|
| ✅ | C4 Model architecture diagrams (context + container) | ⭐ Senior |
| ✅ | Architecture Decision Records (ADRs) | ⭐ Senior |
| ✅ | ML system design doc — scalability & fault tolerance | ⭐ Senior |
| ✅ | Environment strategy (dev / staging / prod isolation) | Standard |

> **★ Senior Differentiator:** C4 Model + ADR usage signals senior-level system design thinking.

**Output:** Architecture docs + C4 diagrams + ADRs

---

## ⚡ Phase 02 — Core ML Pipeline `active` · 3d

**Stack:** scikit-learn / XGBoost · MLflow Tracking · Pandas · Great Expectations

| Status | Task | Level |
|--------|------|-------|
| 🔜 | Dataset selection — Kaggle tabular (fraud detection / churn) | ⭐ Senior |
| 🔜 | Data quality validation with **Great Expectations** | ⭐ Senior |
| 🔜 | Feature engineering pipeline (reusable transforms) | ⭐ Senior |
| 🔜 | **MLflow** experiment tracking (local) | ⭐ Senior |
| 🔜 | Model training + evaluation scripts | Standard |
| 🔜 | Local pipeline test (no cloud) | Standard |

> **★ Senior Differentiator:** Great Expectations + MLflow combination — absent in 90% of portfolios.

**Output:** `training/train.py` · `scripts/preprocess.py` · mlflow tracking

---

## 🔜 Phase 03 — SageMaker Pipeline + Feature Store · 3d

**Stack:** SageMaker Pipelines · SageMaker Feature Store · SageMaker Model Registry · S3

| Status | Task | Level |
|--------|------|-------|
| 🔜 | SageMaker Feature Store setup (offline + online store) | ⭐ Senior |
| 🔜 | Processing Step with data validation | Standard |
| 🔜 | Training Step with **hyperparameter tuning (HPO)** | ⭐ Senior |
| 🔜 | Evaluation Step with **bias detection (Clarify)** | ⭐ Senior |
| 🔜 | Conditional registration — only if accuracy > threshold | ⭐ Senior |
| 🔜 | Model Registry with approval workflow | Standard |

> **★ Senior Differentiator:** Feature Store + SageMaker Clarify (bias detection) makes this enterprise-grade.

**Output:** SageMaker Pipeline · Feature Store · Model Registry

---

## 🔜 Phase 04 — CI/CD — GitHub Actions + OIDC · 2d

**Stack:** GitHub Actions · OIDC Federation · GitHub Environments · Reusable Workflows

| Status | Task | Level |
|--------|------|-------|
| 🔜 | **GitHub OIDC** → AWS role assumption (no access keys) | ⭐ Senior |
| 🔜 | Reusable workflow components (`.github/workflows/shared/`) | ⭐ Senior |
| 🔜 | Build pipeline — lint + test + SageMaker pipeline trigger | Standard |
| 🔜 | Deploy pipeline — staging → approval → production | Standard |
| 🔜 | Pipeline caching for faster builds | ⭐ Senior |
| 🔜 | **Rollback mechanism** on failed deployment | ⭐ Senior |

> **★ Senior Differentiator:** OIDC + rollback mechanism is a strong signal to any recruiter. Using IAM users looks weak by comparison.

**Output:** `.github/workflows/` · OIDC config · rollback scripts

---

## 🔜 Phase 05 — Infrastructure as Code — Terraform · 3d

**Stack:** Terraform · Terragrunt (optional) · tfvars per env · S3 backend

| Status | Task | Level |
|--------|------|-------|
| 🔜 | Terraform modules: S3 · IAM · Lambda · EventBridge · ECR | Standard |
| 🔜 | **Remote state backend** (S3 + DynamoDB locking) | ⭐ Senior |
| 🔜 | Environments: dev · staging · prod isolation | Standard |
| 🔜 | **Terraform CI** — validate + plan on PR, apply on merge | ⭐ Senior |
| 🔜 | SageMaker endpoint infrastructure in Terraform | ⭐ Senior |
| 🔜 | Cost tagging strategy (project / env / owner tags) | ⭐ Senior |

> **★ Senior Differentiator:** Terraform CI (plan on PR) + DynamoDB state locking = production-grade Terraform. Few candidates know this.

**Output:** `terraform/` modules + environments · remote state

---

## 🔜 Phase 06 — Security Hardening · 2d

**Stack:** AWS IAM (least privilege) · OIDC · Secrets Manager · tfsec / checkov

| Status | Task | Level |
|--------|------|-------|
| 🔜 | Least-privilege IAM policies per service | ⭐ Senior |
| 🔜 | **tfsec + checkov** in CI pipeline | ⭐ Senior |
| 🔜 | Secrets rotation strategy (Secrets Manager) | ⭐ Senior |
| 🔜 | VPC endpoint for SageMaker (no public internet) | ⭐ Senior |
| 🔜 | Security architecture documentation | Standard |

> **★ Senior Differentiator:** tfsec/checkov + VPC endpoint signals "this engineer can be trusted with production security."

**Output:** IAM policies · security scan reports · VPC config

---

## 🔜 Phase 07 — Monitoring & Model Observability · 2d

**Stack:** SageMaker Model Monitor · CloudWatch · CloudWatch Dashboard · SNS Alerts

| Status | Task | Level |
|--------|------|-------|
| 🔜 | **SageMaker Model Monitor** — data quality baseline | ⭐ Senior |
| 🔜 | Data drift detection schedule | ⭐ Senior |
| 🔜 | CloudWatch custom metrics (inference latency · error rate) | Standard |
| 🔜 | **Alerting via SNS** — drift detected → notification | ⭐ Senior |
| 🔜 | CloudWatch operational dashboard | Standard |

> **★ Senior Differentiator:** Model Monitor + drift alerting = MLOps maturity level 3. Very few portfolio projects reach this level.

**Output:** Model Monitor config · CloudWatch Dashboard · alerts

---

## 🔜 Phase 08 — Portfolio Polish & Demo · 2d

**Stack:** README.md · GitHub Pages (optional) · Loom demo video · Architecture diagrams

| Status | Task | Level |
|--------|------|-------|
| 🔜 | README — architecture · security · pipeline flow | Standard |
| 🔜 | **GitHub badges** (build status · coverage · terraform) | ⭐ Senior |
| 🔜 | Architecture diagram (C4 export as PNG) | Standard |
| 🔜 | CI/CD screenshot walkthrough | Standard |
| 🔜 | **5-min Loom demo** (pipeline run end-to-end) | ⭐ Senior |
| 🔜 | LinkedIn post about the project | ⭐ Senior |

> **★ Senior Differentiator:** Loom video + LinkedIn post = recruiter watches your system running live. Much stronger than a CV bullet point.

**Output:** Polished README · demo video · LinkedIn draft