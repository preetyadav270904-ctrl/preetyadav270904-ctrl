<div align="center">
<img src="./7.png" width="100%"/>
</div>

<br/>

<div align="center">

[![Kubernetes](https://img.shields.io/badge/Kubernetes-CKA%20Level-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![Terraform](https://img.shields.io/badge/Terraform-Associate-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)](https://www.terraform.io/)
[![AWS](https://img.shields.io/badge/AWS-Cloud-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)](https://aws.amazon.com/)
[![Vault](https://img.shields.io/badge/HashiCorp-Vault-FFEC6E?style=for-the-badge&logo=vault&logoColor=black)](https://www.vaultproject.io/)
[![Docker](https://img.shields.io/badge/Docker-Certified-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Linux](https://img.shields.io/badge/Linux-LFCS%20Level-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://www.linux.org/)

[![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-CI%2FCD-2088FF?style=flat-square&logo=githubactions&logoColor=white)]()
[![KEDA](https://img.shields.io/badge/KEDA-Event%20Driven%20Scaling-ff2d78?style=flat-square)]()
[![Python](https://img.shields.io/badge/Python-ML%20Scripting-3776AB?style=flat-square&logo=python&logoColor=white)]()
[![MySQL](https://img.shields.io/badge/MySQL-Database-4479A1?style=flat-square&logo=mysql&logoColor=white)]()

</div>

---

<div align="center">

### `$ kubectl apply -f career.yaml`

*DevOps & MLOps Engineer · Zero-Trust Security · FinOps Cost Optimization*

</div>

---

## 👋 About Me

I'm a hands-on **DevOps and MLOps Engineer** focused on building production-grade, secure, and hyper-efficient infrastructure. I bypass the theoretical fluff to design resilient, cloud-native ecosystems from scratch.

My engineering philosophy anchors on two pillars:

- 🔐 **Zero-Trust Security** — making infrastructure bulletproof from the ground up
- 💸 **FinOps Cost Optimization** — driving idle resource costs down to absolute zero

---

## 🛠️ Core Tech Stack

| Category | Technologies |
| :--- | :--- |
| **Container Orchestration & OS** | Kubernetes (CKA-level), Docker, K3s, Linux (LFCS-level), Bash |
| **Infrastructure as Code & CI/CD** | Terraform, GitHub Actions, NGINX Ingress |
| **Cloud Infrastructure** | AWS (EC2, S3, SQS, CloudWatch, IAM) |
| **Data & Languages** | Python (ML-focused), MySQL |
| **Specialized Architecture** | KEDA, HashiCorp Vault |

---

## 🚀 Featured Projects

### 1. Multi-Tenant Namespace Shield — HashiCorp Vault 🔒

> *Zero hardcoded credentials. Zero cross-tenant leakage. Zero compromise.*

**The Problem:** In shared Kubernetes clusters, weak RBAC means Tenant A can discover Tenant B's database credentials. Standard Kubernetes Secrets are only Base64 encoded — not encrypted.

**The Solution:** Implemented strict Kubernetes Network Policies for total namespace isolation between `pulkita-workspace` and `preet-workspace`. Integrated HashiCorp Vault on a centralized AWS Commander node to dynamically inject MySQL credentials into running pods at runtime — achieving a true Zero-Trust environment.

```mermaid
graph LR
    subgraph Cluster ["K3s Cluster"]
        subgraph NSA ["Namespace: pulkita"]
            PA[App Pod] --> VA[Vault Agent Sidecar]
        end
        subgraph NSB ["Namespace: preet"]
            PB[App Pod] --> VB[Vault Agent Sidecar]
        end
    end
    VAULT[HashiCorp Vault\nAWS EC2] -->|pulkita/* only| VA
    VAULT -->|preet/* only| VB
    NSA -. "Network Policy\nBLOCKED ❌" .- NSB

    style Cluster fill:#0d0014,color:#fff,stroke:#7B42BC
    style NSA fill:#1a0533,color:#fff,stroke:#ff2d78
    style NSB fill:#1a0533,color:#fff,stroke:#ff2d78
    style VAULT fill:#0d0014,color:#FFEC6E,stroke:#FFEC6E
```

**Key Tech:** `Kubernetes` `HashiCorp Vault` `K3s` `MySQL` `Linux` `AWS EC2`

---

### 2. Scale-to-Zero ML Inference API 📉

> *If no work exists, no cost exists. Idle = $0.00.*

**The Problem:** ML workloads are expensive. Running GPU/compute nodes 24/7 for intermittent inference requests is pure cloud waste.

**The Solution:** Deployed a containerized ML sentiment analysis model integrated with KEDA monitoring an AWS SQS queue. When idle, worker nodes scale entirely to **zero**. When 100+ images hit AWS S3, a Terraform workflow dynamically spins up 3 Spot Workers to handle the burst — then scales back to zero when done.

```mermaid
graph TD
    S3[📦 AWS S3\nImages Uploaded] -->|Event Trigger| SQS[📬 AWS SQS Queue]
    SQS -->|Queue Depth Monitor| KEDA[⚡ KEDA Autoscaler]
    KEDA -->|Queue = 0| ZERO[💤 Workers = 0\nCost = $0.00]
    KEDA -->|Queue > 100| SCALE[🚀 Terraform Spins\n3 Spot Workers]
    SCALE --> ML[🤖 ML Inference\nSentiment / Object Detection]
    ML -->|Queue Drained| ZERO

    style S3 fill:#0d0014,color:#fff,stroke:#FF9900
    style SQS fill:#0d0014,color:#fff,stroke:#FF9900
    style KEDA fill:#1a0533,color:#fff,stroke:#ff2d78
    style ZERO fill:#0a1a0a,color:#fff,stroke:#00d4aa
    style SCALE fill:#1a0533,color:#fff,stroke:#ff2d78
    style ML fill:#0d0014,color:#fff,stroke:#7B42BC
```

**Key Tech:** `KEDA` `Docker` `Python` `Terraform` `AWS SQS` `AWS S3`

---

### 3. CloudWatch-Driven Canary Deployment Engine 🦅

> *Ship fast. Catch failures before users do. Roll back in seconds.*

**The Problem:** Traditional deployments are binary — you're either fully deployed or fully rolled back. There's no safe middle ground to validate new code against real production traffic.

**The Solution:** Engineered a GitHub Actions pipeline that ships v2 of a Python API into a dedicated preview namespace. NGINX Ingress handles smart traffic splitting (10% Canary / 90% Stable). The pipeline actively queries AWS CloudWatch Log Insights for MySQL error strings and HTTP 5xx codes. If error telemetry stays flat for 5 minutes → automatic full promotion. If errors spike → instant automated rollback.

```mermaid
graph TD
    PUSH[📤 Git Push v2] --> GHA[GitHub Actions Pipeline]
    GHA --> DEPLOY[Deploy to\nCanary Namespace]
    DEPLOY --> SPLIT["NGINX Ingress\n10% Canary / 90% Stable"]
    SPLIT --> CW[AWS CloudWatch\nMonitor 5xx + MySQL Errors]
    CW -->|"✅ 0 errors for 5 min"| PROMOTE[100% Traffic → Stable v2]
    CW -->|"🚨 Errors Detected"| ROLLBACK[Instant Automated Rollback]

    style GHA fill:#1a0533,color:#fff,stroke:#ff2d78
    style SPLIT fill:#0d0014,color:#fff,stroke:#7B42BC
    style CW fill:#0d0014,color:#fff,stroke:#FF9900
    style PROMOTE fill:#0a1a0a,color:#fff,stroke:#00d4aa
    style ROLLBACK fill:#1a0014,color:#fff,stroke:#ff2d78
```

**Key Tech:** `GitHub Actions` `NGINX Ingress` `AWS CloudWatch` `Python` `Kubernetes`

---

## 📊 What I'm Building Right Now

- 🏗️ Designing cost-optimized, automated infrastructure blueprints
- 🤖 Bridging the gap between Data Science and Infrastructure with robust MLOps patterns
- ✍️ Documenting engineering breakdowns on [Hashnode](https://yourhashnode.com) · [Dev.to](https://dev.to/yourusername)

---


## 🤝 Let's Connect

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Preet%20Yadav-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/preetyadav319)
[![Dev.to](https://img.shields.io/badge/Dev.to-Blog-0A0A0A?style=for-the-badge&logo=devdotto&logoColor=white)](https://dev.to/preet2709)
[![Hashnode](https://img.shields.io/badge/Hashnode-Blog-2962FF?style=for-the-badge&logo=hashnode&logoColor=white)](https://hashnode.com/@preet2709)
[![Email](https://img.shields.io/badge/Email-Contact-ff2d78?style=for-the-badge&logo=gmail&logoColor=white)](mailto:preetyadav270904@gmail.com)

</div>

<br/>

<div align="center">

*"Production-ready execution over theory. Let's build something scalable."*

</div>

<div align="center">
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:ff2d78,50:7B42BC,100:0d0014&height=120&section=footer&animation=fadeIn" width="100%"/>
</div>
