## AI Cloud Cost Detective
  
An AI-powered tool that investigates AWS cloud costs automatically. It scans resources in an AWS Account/Region, detects cost issues like over-provisioning and misconfigurations, and provides actionable suggestions with fixes.

### Tech Stack

<table>
<tr>
<th>  
Layer
</th>
<th>  
Technology
</th>
</tr>
<tr>
<td>  
Frontend
</td>
<td>  
React (Vite + TypeScript + Tailwind)
</td>
</tr>
<tr>
<td>  
Backend
</td>
<td>  
Python (FastAPI)
</td>
</tr>
<tr>
<td>  
Auth
</td>
<td>  
Custom JWT Auth (bcrypt + PyJWT)
</td>
</tr>
<tr>
<td>  
Cloud Data
</td>
<td>  
AWS SDK (Boto3)
</td>
</tr>
<tr>
<td>  
Cloud
</td>
<td>  
AWS
</td>
</tr>
<tr>
<td>  
AI Analysis
</td>
<td>  
Google AI Studio (Gemini API)
</td>
</tr>
<tr>
<td>  
Database
</td>
<td>  
Amazon RDS PostgreSQL
</td>
</tr>
<tr>
<td>  
Live Updates
</td>
<td>  
FastAPI WebSocket
</td>
</tr>
</table>


### Architecture
                              ┌──────────────┐
                              │     USER     │
                              └──────┬───────┘
                                     │
                                     ▼
                           ┌───────────────────┐
                           │  REACT FRONTEND   │
                           └────────┬──────────┘
                                    :
                                    : Login / Signup
                                    ▼
                           ┌───────────────────┐
                           │  PYTHON BACKEND   │
                           │    (FastAPI)      │
                           │                   │
                           │  · Custom JWT Auth│
                           └───┬───────┬───┬───┘
                               :       :   :
                ┌──────────────┘       :   └──────────────┐
                :                      :                  :
                ▼                      ▼                  ▼
         ┌─────────────┐     ┌──────────────┐    ┌──────────────┐
         │  AWS SDK    │     │   FASTAPI    │    │  GOOGLE AI   │
         │  (BOTO3)    │     │  WEBSOCKET   │    │   STUDIO     │
         │             │     │  (Progress)  │    │ (Gemini API) │
         │ boto3       │     └──────┬───────┘    │              │
         │ describe_*  │            :            │ Cost Analysis│
         └──────┬──────┘            :            └──────┬───────┘
                :                   : Live updates      :
                ▼                   ▼                   :
         ┌─────────────┐   ┌───────────────┐            :
         │    AWS      │   │    REACT      │            :
         │ (Account /  │   │  (Progress    │            :
         │  Region)    │   │   Tracker)    │            :
         └─────────────┘   └───────────────┘            :
                                                        ▼
                                                 ┌──────────────┐
                                                 │   AMAZON     │
                                                 │     RDS      │
                                                 │ (PostgreSQL) │
                                                 │              │
                                                 │ · users      │
                                                 │ · analyses   │
                                                 └──────┬───────┘
                                                        :
                                                        : Stored results
                                                        ▼
                                                 ┌───────────────┐
                                                 │    REACT      │
                                                 │ (Final Report │
                                                 │  + Suggestions│
                                                 │  + Fixes)     │
                                                 └───────────────┘

### Request Flow
①  User ─·─·─► React ─·─·─► FastAPI Auth ─·─·─► JWT (Amazon RDS PostgreSQL)
②  User selects AWS Region / Account ─·─·─► Python Backend
③  Python ─·─·─► Boto3 ─·─·─► Fetches all resources in Account/Region
④  Python ─·─·─► FastAPI WebSocket ─·─·─► React (live progress)
⑤  Python ─·─·─► Google Gemini API ─·─·─► Cost analysis
⑥  Python ─·─·─► Amazon RDS PostgreSQL ─·─·─► Stores analysis history
⑦  React ◄·─·─·─ Final report with suggestions & fixes

### What It Detects
- **Over-provisioned resources** — EC2 instances, RDS databases, or Lambda functions sized larger than needed
- **Unused resources** — Unattached EBS volumes, unused Elastic IPs, idle load balancers
- **Misconfigurations** — Wrong instance types, missing auto-stop schedules, no Reserved Instances or Savings Plans
- **Storage & logging costs** — Excessive CloudWatch log retention, no S3 lifecycle policies on bucket storage

### Prerequisites
- AWS CLI installed and configured (aws configure)
- An active AWS account with at least one region containing resources
- An Amazon RDS PostgreSQL instance
- A Google AI Studio API key
- Python 3.10+
- Node.js 18+

### How to Run

#### Backend
cd backend
pip install -r requirements.txt
cp .env.example .env   # fill in your credentials
uvicorn main:app --reload

#### Frontend
cd frontend
npm install
npm run dev

### How It Works
- User signs up / logs in via custom JWT auth (credentials stored in Amazon RDS PostgreSQL)
- Selects an AWS Region / Account to analyze
- Python backend fetches all resources using Boto3
- Live progress is streamed to the UI via FastAPI WebSocket
- Resource data is sent to Google Gemini API for cost analysis
- Analysis results are stored in Amazon RDS PostgreSQL
- Final report with cost breakdown, suggestions, and fix commands is displayed