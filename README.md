# 🤖 Multi-Agent Autonomous Enterprise Data Platform

> **6 autonomous agents. One platform. Zero data chaos.**

An intelligent, agent-driven platform that automates the complete lifecycle of enterprise data — from raw ingestion to governed distribution. Built with **6 specialized AI agents** orchestrated in real-time, powered by **FastAPI**, **React**, **SQLite**, and **Google Gemini**.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [The Six Agents](#-the-six-agents)
- [Architecture](#-architecture)
- [Tech Stack](#-tech-stack)
- [Features](#-features)
- [Project Structure](#-project-structure)
- [Database Schema](#-database-schema)
- [Installation & Setup](#-installation--setup)
- [API Endpoints](#-api-endpoints)
- [Screenshots](#-screenshots)
- [How It Works](#-how-it-works)
- [Use Cases](#-use-cases)
- [Future Scope](#-future-scope)
- [Author](#-author)
- [License](#-license)

---

## 🎯 Overview

Traditional data pipelines rely on rigid scripts and manual intervention — making them slow, error-prone, and hard to scale. This project reimagines that workflow by deploying **six specialized autonomous agents** that collaborate through a central orchestrator to **ingest, clean, validate, transform, catalog, and govern** enterprise data with minimal human oversight.

The platform provides a **real-time dashboard** where users can watch agents execute live, view quality scores, browse the metadata catalog, and inspect governance/PII reports — turning a black-box pipeline into a **transparent, observable workflow**.

---

## 🤖 The Six Agents

| # | Agent | Responsibility |
|---|-------|----------------|
| 1️⃣ | **Ingestion Agent** | Accepts CSV/JSON/Excel files, loads them into a structured DataFrame, captures source metadata |
| 2️⃣ | **Validation Agent** | Verifies schema integrity, required columns, and data type conformity |
| 3️⃣ | **Quality Agent** | Detects nulls, duplicates, outliers, inconsistencies; computes quality score (0–100) |
| 4️⃣ | **Transformation Agent** | Cleans data — fills nulls, removes duplicates, normalizes formats, applies AI-suggested transforms |
| 5️⃣ | **Metadata Agent** | Auto-generates a searchable data catalog with column descriptions (powered by Gemini) |
| 6️⃣ | **Governance Agent** | Detects PII (email, phone, PAN, Aadhaar), applies compliance rules, produces risk reports |

🎛️ **Orchestrator** — A central controller that coordinates all 6 agents sequentially, logs every step, and exposes real-time status to the frontend.

---

## 🏗️ Architecture



---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Backend** | Python 3.11+, FastAPI, Uvicorn | REST API & orchestration |
| **AI Layer** | Google Gemini API | Metadata generation, PII reasoning, smart transforms |
| **Data Processing** | Pandas, NumPy | Ingestion, cleaning, profiling |
| **ORM** | SQLAlchemy | Database models |
| **Validation** | Pydantic | Request/response schemas |
| **Database** | SQLite | Lightweight, CPU-friendly storage |
| **Frontend** | React 18, Vite | SPA framework |
| **Styling** | TailwindCSS | Modern, utility-first design |
| **Animations** | Framer Motion | Agent pipeline animation |
| **Charts** | Recharts | Quality analytics visualization |
| **Icons** | Lucide React | Clean icon set |
| **Routing** | React Router DOM | Page navigation |
| **HTTP Client** | Axios | API communication |

> ⚡ **Optimized for CPU-only machines** — uses cloud LLM inference (Gemini) instead of local GPU models, making it accessible to students and developers without high-end hardware.

---

## ✨ Features

### 🔄 End-to-End Automation
- 6 agents process data autonomously from upload → final clean output
- Sequential orchestration with dependency handling
- Failure recovery and detailed error logging

### 📊 Real-Time Visualization
- Animated 6-agent pipeline flow
- Live status indicators (pending / running / completed / failed)
- Real-time agent logs in a terminal-style viewer
- Duration tracking per agent

### 🧹 Data Quality & Cleaning
- Null detection & intelligent imputation
- Duplicate removal
- Outlier detection (Z-score method)
- Data type validation & correction
- Quality score (0–100) with breakdown

### 🔍 Metadata Catalog
- Auto-generated column descriptions via Gemini
- Data type, null %, unique count, sample values
- Searchable & filterable catalog table

### 🛡️ Governance & Compliance
- PII detection (email, phone, PAN, Aadhaar, credit card)
- Risk level classification (Low / Medium / High)
- GDPR-style compliance report
- Actionable recommendations

### 📁 Multi-Format Support
- CSV, JSON, Excel file uploads
- Drag-and-drop UI
- File preview before processing

### 💾 Export & Download
- Download cleaned dataset
- Export quality report
- Export governance report

---

## 📁 Project Structure



---

## 🗄️ Database Schema

### Tables

**1. `datasets`** — Uploaded dataset info
| Column | Type | Description |
|--------|------|-------------|
| id | INTEGER PK | Dataset ID |
| filename | TEXT | Original filename |
| filepath | TEXT | Storage path |
| rows | INTEGER | Row count |
| columns | INTEGER | Column count |
| uploaded_at | DATETIME | Upload timestamp |
| status | TEXT | pending / processing / done |

**2. `pipeline_runs`** — Pipeline execution record
| Column | Type | Description |
|--------|------|-------------|
| id | INTEGER PK | Run ID |
| dataset_id | INTEGER FK | Reference to dataset |
| started_at | DATETIME | Start time |
| completed_at | DATETIME | End time |
| overall_status | TEXT | running / success / failed |
| current_agent | TEXT | Active agent name |

**3. `agent_logs`** — Per-agent logs
| Column | Type | Description |
|--------|------|-------------|
| id | INTEGER PK | Log ID |
| run_id | INTEGER FK | Pipeline run reference |
| agent_name | TEXT | Agent identifier |
| status | TEXT | pending / running / done / failed |
| message | TEXT | Log message |
| duration_ms | INTEGER | Execution time |
| started_at | DATETIME | Start time |
| completed_at | DATETIME | End time |

**4. `quality_reports`** — Quality metrics
| Column | Type | Description |
|--------|------|-------------|
| id | INTEGER PK | Report ID |
| run_id | INTEGER FK | Pipeline run reference |
| total_rows | INTEGER | Total rows |
| null_count | INTEGER | Null cells |
| duplicate_count | INTEGER | Duplicate rows |
| outlier_count | INTEGER | Outliers detected |
| quality_score | FLOAT | 0–100 |
| details_json | TEXT | Detailed breakdown |

**5. `metadata_catalog`** — Column catalog
| Column | Type | Description |
|--------|------|-------------|
| id | INTEGER PK | Catalog entry ID |
| run_id | INTEGER FK | Pipeline run reference |
| column_name | TEXT | Column name |
| data_type | TEXT | Detected type |
| description | TEXT | AI-generated description |
| null_percent | FLOAT | % nulls |
| unique_count | INTEGER | Unique values |
| sample_values | TEXT | Sample data |

**6. `governance_reports`** — Compliance & PII
| Column | Type | Description |
|--------|------|-------------|
| id | INTEGER PK | Report ID |
| run_id | INTEGER FK | Pipeline run reference |
| pii_columns_json | TEXT | Detected PII columns |
| risk_level | TEXT | Low / Medium / High |
| compliance_status | TEXT | Pass / Fail |
| recommendations | TEXT | Action items |

---

## 🚀 Installation & Setup

### Prerequisites

- **Python** 3.11 or higher
- **Node.js** 18 or higher
- **npm** or **yarn**
- **Google Gemini API Key** → [Get it here](https://aistudio.google.com/apikey)
- **Git**

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/vishakha2121/Multi-Agent-Autonomous-Enterprise-Data-Platform.git
cd Multi-Agent-Autonomous-Enterprise-Data-Platform


cd backend

# Create virtual environment
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (Mac/Linux)
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt


cd frontend
npm install