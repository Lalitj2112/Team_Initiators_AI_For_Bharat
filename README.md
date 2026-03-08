# 🌿 TerraOS — AI-Powered Soil Intelligence Platform

> **Smart Soil. Better Harvest. For Every Indian Farmer.**

[![AWS](https://img.shields.io/badge/AWS-Powered-FF9900?style=flat&logo=amazonaws)](https://aws.amazon.com)
[![Bedrock](https://img.shields.io/badge/Amazon-Bedrock-232F3E?style=flat&logo=amazonaws)](https://aws.amazon.com/bedrock)
[![Region](https://img.shields.io/badge/Region-ap--south--1-blue?style=flat)](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/)
[![Languages](https://img.shields.io/badge/Languages-7%20Indian-green?style=flat)](.)
[![Analysis](https://img.shields.io/badge/Analysis%20Time-60%20seconds-brightgreen?style=flat)](.)

---

## 📋 Table of Contents

- [What is TerraOS?](#-what-is-terraos)
- [The Problem](#-the-problem)
- [Our Solution](#-our-solution)
- [System Architecture](#-system-architecture)
- [AI Agent Pipeline](#-ai-agent-pipeline)
- [Data Lake Architecture](#-data-lake-architecture)
- [AWS Services](#-aws-services)
- [Getting Started](#-getting-started)
- [API Reference](#-api-reference)
- [Project Structure](#-project-structure)
- [Hackathon Highlights](#-hackathon-highlights)

---

## 🌱 What is TerraOS?

TerraOS transforms basic soil test values (N, P, K, pH) into a comprehensive agricultural intelligence report in under **couple of minutes** — powered by a 5-agent Amazon Bedrock pipeline running on AWS serverless infrastructure.

```
Farmer enters 4 values  →  5 AI agents analyze  →  Full report in couple of minutes
N, P, K, pH                NPK + Ecosystem           Carbon credits
                           Suggestions               Regenerative practices
                           Historical trends         6 languages
```

---

## 🚜 The Problem

| Challenge | Scale |
|-----------|-------|
| Indian farmers | **140 million+** |
| Yield lost to poor soil management | **15–40%** |
| Farmers without soil testing access | **60%** |
| Lab test cost + wait time | **$ 6–22(approx) + 2–4 weeks** |
| Carbon credit awareness | **< 1%** of eligible farmers |

> Indian farmers did not know about carbon credit income.

---

## 💡 Our Solution

TerraOS provides **instant, affordable, multilingual soil intelligence** — no lab required.

```
┌─────────────────────────────────────────────────────────────────┐
│                         TerraOS                                 │
│                                                                 │
│  INPUT            AI PIPELINE           OUTPUT                  │
│  ─────            ───────────           ──────                  │
│  N: 110  ──────→  NPK Agent      ──────→  Soil Score: 78/100    │
│  P: 130           Ecosystem Agent         Grade: B              │
│  K: 167           Suggestion Agent        Carbon:Eligible or not│
│  pH: 6.8          Historical Agent        3 Priority Actions    │
│                   Carbon Agent            6 Languages           │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🏗️ System Architecture

### High-Level Flow

```
┌──────────┐      ┌─────────────┐      ┌──────────────┐      ┌─────────────────┐
│  React   │      │  API Gateway│      │  Cognito JWT │      │  Lambda         │
│  Web App │────▶│  REST API    │────▶│  Authorizer  │────▶│  api-handler    │
│          │      │  ap-south-1 │      │              │      │                 │
└──────────┘      └─────────────┘      └──────────────┘      └────────┬────────┘
                                                                     │
                                                                     ▼
                                                           ┌─────────────────┐
                                                           │  S3 Bronze      │
                                                           │  inputs/        │
                                                           │  FARMER_ID/     │
                                                           │  FARMER_TS.json │
                                                           └────────┬────────┘
                                                                     │
                                                                     ▼
                                                           ┌─────────────────┐
                                                           │  Lambda         │
                                                           │  input-trigger  │
                                                           │  (S3 event)     │
                                                           └────────┬────────┘
                                                                     │
                                                                     ▼
                                                           ┌──────────────────┐
                                                           │  AWS Glue Job 1  │
                                                           │  Bronze Cleaner  │
                                                           │  • Null check    │
                                                           │  • Range validate│
                                                           └────────┬─────────┘
                                                                    │
                                                                    ▼
                                                           ┌─────────────────┐
                                                           │  Step Functions │
                                                           │  Orchestrator   │
                                                           └────────┬────────┘
                                                                    │
                              ┌─────────────────────────────────────┤
                              │              PARALLEL               │
                              ▼                                     ▼
                    ┌─────────────────┐                   ┌─────────────────┐
                    │  Lambda         │                   │  Lambda         │
                    │  npk-agent      │                   │  nutrient-agent │
                    │  (Bedrock)      │                   │  (Bedrock)      │
                    └────────┬────────┘                   └──────────┬──────┘
                              │                                      │
                              └──────────────┬───────────────────────┘
                                             │
                                             ▼
                                   ┌──────────────────┐
                                   │  Lambda          │
                                   │  suggestion-agent│
                                   │  (Bedrock)       │
                                   │  → S3 Silver     │
                                   │  → Glue Job 2    │
                                   └────────┬─────────┘
                                            │
                                            ▼
                                   ┌──────────────────┐
                                   │  Lambda          │
                                   │  historical-agent│
                                   │  (reads S3)      │
                                   │  (Bedrock)       │
                                   └────────┬─────────┘
                                            │
                                            ▼
                                   ┌──────────────────┐
                                   │  Lambda          │
                                   │  carbon-agent    │
                                   │  (Bedrock)       │
                                   │  → S3 Gold       │
                                   │  → DynamoDB      │
                                   │  → Glue Job 3    │
                                   └────────┬─────────┘
                                            │
                                            ▼
                                   ┌──────────────────┐               
                                   │  report-fetcher  │
                                   │  S3 Gold read    │      
                                   └────────┬─────────┘
                                            │
                                            ▼
                                   ┌─────────────────┐
                                   │ Rendering Report│
                                   │  to UI          │
                                   └─────────────────┘
```

---

## 🤖 AI Agent Pipeline

### 5 Specialist Agents

```
                        ┌──────────────────────────────┐
                        │     SOIL DATA INPUT          │
                        │  N=110, P=130, K=167, pH=6.8 │
                        └──────────────┬───────────────┘
                                       │
                    ┌──────────────────┼
                    │                  │                   
                    ▼                  ▼                   
          ┌─────────────────┐ ┌────────────────────┐         
          │  🧪 NPK AGENT   │ │ 🌍 Nutrient       │         
          │                 │ │    AGENT           │         
          │ • N/P/K status  │ │                    │         
          │ • pH assessment │ │ • Micronutrients   │         
          │ • NPK score     │ │ • Organic carbon   │         
          │ • Fertilizer    │ │ • Microbial health │         
          │   recs          │ │                    │      
          └────────┬────────┘ └────────┬───────────┘         
                   │                   │                   
                   └─────────┬─────────┘                   
                             │                             
                             ▼                             
                   ┌─────────────────┐                     
                   │ 💡 SUGGESTION   │                    
                   │    AGENT        │                     
                   │                 │                     
                   │ • Soil score    │                     
                   │ • Grade (A-F)   │
                   │ • Priority acts │
                   │ • Crop recs     │
                   │ → S3 Silver     │
                   └────────┬────────┘
                            │
                            ▼
                   ┌─────────────────┐
                   │ 📈 HISTORICAL   │
                   │    AGENT        │
                   │                 │
                   │ • Reads past    │
                   │   reports       │
                   │ • Trend: ↑↓→    │
                   │ • Compares N/P/K│
                   │ • Adjusted recs │
                   └────────┬────────┘
                            │
                            ▼
                   ┌─────────────────┐
                   │ 🌱 CARBON       │
                   │    AGENT        │
                   │                 │
                   │ • CO2 potential │
                   │ • Programs      │
                   │ • Payback period│
                   │ → S3 Gold       │
                   └─────────────────┘
```

### Agent Retry Strategy

```
Attempt 1 ──▶ [Bedrock call]
     │              │
     │         ✅ Success ──▶ Parse JSON ──▶ Return
     │
     ▼ Throttling/Timeout
Attempt 2 ──▶ wait 2s + jitter ──▶ [Bedrock call]
     │
     ▼ Throttling/Timeout
Attempt 3 ──▶ wait 4s + jitter ──▶ [Bedrock call]
     │
     ▼ Throttling/Timeout
Attempt 4 ──▶ wait 8s + jitter ──▶ [Bedrock call]
     │
     ▼ Still failing
  Raise exception ──▶ Step Functions catches ──▶ Error state
```

---

## 🗄️ Data Lake Architecture

### S3 Layer Structure

```
terraos.bucket.bronze/
├── inputs/
│   └── {farmer_id}/
│       └── {farmer_id}_{YYYY-MM-DDTHH-MM-SSZ}.json        ← Raw input
└── cleaned/
│    └── {farmer_id}/
│        └── {farmer_id}_{YYYY-MM-DDTHH-MM-SSZ}_cleaned.json ← Glue Job 1
│
└──glue-scripts/
    └── glue_bronze_cleaner.py

terraos.bucket.silver/
├── reports/
│   └── {farmer_id}/
│       └── {farmer_id}_{YYYY-MM-DDTHH-MM-SSZ}_silver.json  ← NPK + Suggestions
└── glue-scripts/
    └── glue_silver_filter.py

terraos.bucket.gold/
├── final-reports/
│   └── {farmer_id}/
│       └── {farmer_id}_{YYYY-MM-DDTHH-MM-SSZ}_gold.json    ← Final report
└── glue-scripts/
    └── glue_gold_minifier.py
```

### Glue ETL Pipeline

```
┌─────────────────────────────────────────────────────────────────┐
│                        GLUE ETL JOBS                            │
│                                                                 │
│  Job 1: Bronze Cleaner          Job 2: Silver Filter            │
│  ─────────────────────          ──────────────────              │
│  Input:  inputs/...             Input:  reports/...             │
│  ┌─────────────────┐            ┌──────────────────┐            │
│  │ • Null/NA check │            │ • Keep only      │            │
│  │ • Range validate│            │   historical     │            │
│  │   N: 0-600      │            │   fields         │            │
│  │   P: 0-200      │            │ • Strip full NPK │            │
│  │   K: 0-600      │            │   analysis       │            │
│  │   pH: 0-14      │            │ • Score + grade  │            │
│  │ • Flag issues   │            │   only           │            │
│  │ • No defaults   │            │                  │            │
│  └─────────────────┘            └──────────────────┘            │ 
│  Output: cleaned/...                                            │
│                                                                 │
│  Job 3: Gold Minifier                                           │
│  ──────────────────                                             │
│  Input:  final-reports/...                                      │
│  ┌──────────────────────────────────────────────────┐           │
│  │ • Remove raw Bedrock output                      │           │
│  │ • Keep: soil_health, npk, carbon, historical     │           │
│  │ • Deduplicate lists                              │           │
│  │ • React-ready format                             │           │
│  └──────────────────────────────────────────────────┘           │
│  Output:  (cleaner version)                                     │
└─────────────────────────────────────────────────────────────────┘
```

---

## ☁️ AWS Services

| Service | Purpose | Config |
|---------|---------|--------|
| **Amazon Bedrock** | 5 AI agents | `amazon.nova-pro-v1:0` · `us-east-1` |
| **AWS Lambda** | 8 functions | Python 3.12 · 128–256MB |
| **Step Functions** | Pipeline orchestration | Express workflow |
| **Amazon S3** | Data lake (3 buckets) | Bronze / Silver / Gold |
| **AWS Glue** | ETL cleaning | Python Shell · 0.0625 DPU |
| **DynamoDB** | Report metadata | On-demand · `ap-south-1` |
| **Cognito** | Auth | Email OTP + JWT |
| **API Gateway** | REST API | Cognito authorizer |
| **Amplify** | Frontend hosting | React/Vite build |
| **Amazon Translate** | 6-language support | Real-time |
| **CloudWatch** | Logging | All Lambda + Glue |

### Lambda Function Timeouts

| Function | Timeout | Memory | Reason |
|----------|---------|--------|--------|
| `api-handler` | 30s | 128MB | S3 + DynamoDB write |
| `input-trigger` | 5 min | 128MB | Waits for Glue  |
| `npk-agent` | 2 min | 128MB | Bedrock + retries |
| `nutrient-agent` | 2 min | 128MB | Bedrock + retries |
| `suggestion-agent` | 3 min | 128MB | Bedrock + S3 + Glue trigger |
| `historical-agent` | 3 min | 128MB | S3 list + Bedrock |
| `carbon-agent` | 3 min | 128MB | Bedrock + S3 + DynamoDB + Glue |
| `report-fetcher` | 30s | 128MB | S3 list + reads |

---

## 🚀 Getting Started

### Prerequisites

```bash
# AWS CLI configured
aws configure

# Create S3 buckets
aws s3 mb s3://terraos.bucket.bronze --region ap-south-1
aws s3 mb s3://terraos.bucket.silver --region ap-south-1
aws s3 mb s3://terraos.bucket.gold   --region ap-south-1

# Create DynamoDB table
aws dynamodb create-table \
  --table-name terraos-users \
  --attribute-definitions AttributeName=farmer_id,AttributeType=S \
  --key-schema AttributeName=farmer_id,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST \
  --region ap-south-1
```

### Deploy Lambda Functions

```bash
# Deploy all 8 functions (in order)
1. terraos-api-handler          # API entry point
2. terraos-input-trigger        # S3 event → Glue → Step Functions
3. terraos-npk-agent            # NPK analysis
4. terraos-other-nutrient-agent # Ecosystem analysis
5. terraos-suggestion-agent     # Recommendations + Silver save
6. terraos-historical-agent     # Trend analysis
7. terraos-carbon-agent         # Carbon calc + Gold save
8. terraos-report-fetcher       # Report fetcher
```

### Environment Variables

| Lambda | Variable | Value |
|--------|----------|-------|
| `input-trigger` | `STEP_FUNCTION_ARN` | ARN of your state machine |
| All agents | `AWS_BEDROCK_ACCESS_KEY` | Bedrock IAM key |
| All agents | `AWS_BEDROCK_SECRET_KEY` | Bedrock IAM secret |

### Upload Glue Scripts

```bash
# Upload Glue scripts to respective buckets
aws s3 cp glue_bronze_cleaner.py s3://terraos.bucket.bronze/glue-scripts/
aws s3 cp glue_silver_filter.py  s3://terraos.bucket.silver/glue-scripts/
aws s3 cp glue_gold_minifier.py  s3://terraos.bucket.gold/glue-scripts/
```

### Create Glue Jobs (Console)

For each job:
- Type: **Python Shell**
- Python version: **3.9**
- Max capacity: **0.0625 DPU**
- Timeout: **5 minutes**

---

## 📡 API Reference

### Submit Soil Analysis

```http
POST /analyze
Authorization: Bearer {cognito_jwt}
Content-Type: application/json

{
  "nitrogen": 110,
  "phosphorus": 130,
  "potassium": 167,
  "ph": 6.8,
  "crop_type": "Cotton",
  "location": "Jaipur, Rajasthan",
  "soil_type": "Sandy Loam",
  "farm_size_acres": 2
}
```

**Response:**
```json
{
  "success": true,
  "farmer_id": "41733daa-...",
  "report_id": "be93dec1-...",
  "timestamp": "2026-03-06T04-43-54Z",
}
```

### Fetch Latest Report

```http
GET /report/{farmerId}?latest=true
Authorization: Bearer {cognito_jwt}
```

**Response (complete):**
```json
{
  "status": "complete",
  "report": {
    "soil_health": { "score": 78, "grade": "B" },
    "npk": { "n_status": "adequate", "p_status": "adequate" },
    "carbon": { "potential_income_inr": 28000 },
    "historical": { "trend": "improving" }
  }
}
```

**Response (processing):**
```json
{
  "status": "processing",
  "message": "Analysis in progress..."
}
```

### Fetch All Reports

```http
GET /report/{farmerId}
Authorization: Bearer {cognito_jwt}
```

---

## 📁 Project Structure

```
terraos/
── 📁 src/
│   │
│   ├── 📁 components/                        # Reusable UI components
│   │   ├── ⚛️  BottomNav.jsx                 # Mobile bottom navigation bar
│   │   ├── ⚛️  CarbonCard.jsx                # Carbon credit income display card
│   │   ├── ⚛️  NutrientCard.jsx              # NPK & micronutrient status card
│   │   ├── ⚛️  PracticeAccordion.jsx         # Expandable regenerative practices list
│   │   ├── ⚛️  ProtectedRoute.jsx            # Auth guard — redirects unauthenticated users
│   │   ├── ⚛️  SoilScoreGauge.jsx            # Animated circular soil score gauge (0-100)
│   │   └── ⚛️  TopNav.jsx                    # Top navigation with language switcher
│   │
│   ├── 📁 context/                           # React global state providers
│   │   ├── ⚛️  AuthContext.jsx               # Cognito auth state — user, token, signIn/Out
│   │   └── ⚛️  LanguageContext.jsx           # Active language + translation switcher
│   │
│   ├── 📁 pages/                             # Full-page route components
│   │   ├── ⚛️  AnalyzePage.jsx               # Soil input form → calls POST /analyze
│   │   ├── ⚛️  HistoryPage.jsx               # All past reports → calls GET /report/{id}
│   │   ├── ⚛️  HomePage.jsx                  # Landing + soil score summary dashboard
│   │   ├── ⚛️  LoadingPage.jsx               # 60s polling screen while agents process
│   │   ├── ⚛️  LoginPage.jsx                 # Cognito email OTP login + signup
│   │   ├── ⚛️  ProfilePage.jsx               # Farmer profile + grade + report count
│   │   └── ⚛️  ReportPage.jsx                # Full soil intelligence report view
│   │
│   ├── 📁 services/                          # API & external service connectors
│   │   │                                     # ┌───────────────────────────────────────┐
│   │   ├── 📄  api.js                       # │ Connects to API Gateway REST API       │
│   │   │                                     # │ • POST /analyze  → submit soil data   │
│   │   │                                     # │ • GET  /report/{farmerId}?latest=true │
│   │   │                                     # │ • GET  /report/{farmerId}  (all)      │
│   │   │                                     # │ Attaches Cognito JWT Bearer token     │
│   │   │                                     # │ Endpoint: execute-api.ap-south-1      │
│   │   │                                     # └───────────────────────────────────────┘
│   │   │                                     # ┌─────────────────────────────────────┐
│   │   └── 📄  translateService.js           # │ Connects to Amazon Translate        │
│   │                                         # │ • Translates full report JSON       │
│   │                                         # │ • Supports 6 Indian languages       │
│   │                                         # │ • Caches translations in memory     │
│   │                                         # └─────────────────────────────────────┘
│   │
│   ├── 📁 styles/
│   │   └── 🎨  global.css                    # Global CSS — fonts, colors, base styles
│   │
│   ├── 📁 translations/                      # i18n language files
│   │   ├── 📄  en.js                         # English (default)
│   │   ├── 📄  hi.js                         # Hindi — हिन्दी
│   │   ├── 📄  mr.js                         # Marathi — मराठी
│   │   ├── 📄  ta.js                         # Tamil — தமிழ்
│   │   ├── 📄  te.js                         # Telugu — తెలుగు
│   │   └── 📄  bn.js                         # Bengali — বাংলা
│   │
│   ├── ⚛️  App.jsx                           # Root component — routes + providers
│   ├── 📄  aws-config.js                     # Amplify + Cognito + API Gateway config
│   └── ⚛️  main.jsx                          # Vite entry point
│
├── 🔒  .env                                  # Local env vars (never commit)
├── 📄  .env.example                          # Template for env setup
├── 🌐  index.html                            # Vite HTML shell
├── 📦  package.json                          # Dependencies
├── 📦  package-lock.json                     # Lock file
└── ⚙️  postcss.config.js                     # PostCSS / Tailwind config
│
└── 📁dist/                                   # Production build
│
├── 📁backend/                                # Backend code
│   ├── 📁lambda/                                 # 8 Lambda functions
│   │   ├── 📁api_handler/
│   │   │   └── 🐍lambda_function.py
│   │   ├── 📁input_trigger/
│   │   │   └── 🐍lambda_function.py
│   ├── 📁npk_agent/
│   │   └──🐍 lambda_function.py
│   ├── 📁nutrient_agent/
│   │   └── 🐍lambda_function.py
│   ├── 📁suggestion_agent/
│   │   └── 🐍lambda_function.py
│   ├──📁 historical_agent/
│   │   └──🐍 lambda_function.py
│   ├── 📁carbon_agent/
│   │   └── 🐍lambda_function.py
│   └── 📁report_fetcher/
│   │   └── 🐍lambda_function.py
│   │
│   ├──📁 glue/                       # ETL cleaning scripts
│   │   ├── 🐍glue_bronze_cleaner.py
│   │   ├── 🐍glue_silver_filter.py
│   │   └── 🐍glue_gold_minifier.py

```

---

## 🏆 Hackathon Highlights

### AWS AI for Bharat — Key Innovations

```
┌─────────────────────────────────────────────────────────┐
│              INNOVATION HIGHLIGHTS                      │
│                                                         │
│  1. ZERO-LAB ANALYSIS                                   │
│     AI infers micronutrients, organic carbon, CEC       │
│     from just 4 basic soil parameters                   │
│                                                         │
│  2. CARBON ECONOMY ACCESS                               │
│     First platform connecting farmers to                │
│     Gold Standard, VCS, Plan Vivo programs              │
│                                                         │
│  3. MULTILINGUAL BY DESIGN                              │
│     Hindi · Tamil · Telugu · Marathi                    │
│     Bengali  · English                                  │
│                                                         │
│  4. REGENERATIVE FOCUS                                  │
│     Recommendations prioritize soil health              │
│     improvement, not just chemical fixes                │
│                                                         │
│  5. SERVERLESS + AFFORDABLE                             │
│     Zero infrastructure cost for farmer                 │
│                                                         │
│  6. DATA SOVEREIGNTY                                    │
│     Per-farmer S3 isolation by farmer_id prefix         │
│     No cross-farmer data contamination                  │
└─────────────────────────────────────────────────────────┘
```

### Target Impact

- **140M+** farmers in India
- **60%** currently without soil testing access
- **Eligilibity** for carbon credit identified per farmer
- **15–40%** yield improvement with proper soil management

---

<div align="center">

**🌿 TerraOS — Transforming Indian Agriculture with AI**

*Smart Soil. Better Harvest. For Every Farmer.*

`ap-south-1` · `Amazon Bedrock` · `Serverless` · `Made for Bharat`

</div>
