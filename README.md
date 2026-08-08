<!--
---
title: "VulnScribe | Offline AI-Powered VAPT Reporting Engine"
meta_title: "VulnScribe | Offline VAPT Reporting Engine by Bhavy Morvadiya"
meta_description: "Secure, 100% offline, AI-powered VAPT report generator by Bhavy Morvadiya (kkaxh1). Automatically train on previous reports to generate editable Word documents (.docx) for Web, API, Mobile, Network, and Active Directory audits."
keywords: "Bhavy Morvadiya, Bhavya Morvadiya, kkaxh1, VulnScribe, VAPT reporting tool, offline pentest report builder, AI vulnerability reporting, automated penetration testing report generator, offline RAG security reporting, editable docx pentest reports, Active Directory assessment tool, cybersecurity report automation"
author: "Bhavy Morvadiya"
canonical: "https://bhavymorvadiya.netlify.app/projects/vulnscribe"
og_type: "website"
og_url: "https://bhavymorvadiya.netlify.app/projects/vulnscribe"
og_title: "VulnScribe | Offline AI-Powered VAPT Reporting Engine by Bhavy Morvadiya"
og_description: "Automatically compile professional, NDA-compliant VAPT reports locally using secure AI trained on your previous data."
og_image: "https://bhavymorvadiya.netlify.app/bhavy_3d_avatar.png"
twitter_card: "summary_large_image"
twitter_site: "@kkaxh1"
twitter_creator: "@kkaxh1"
---
-->

# VulnScribe

**Offline AI-assisted VAPT report generation**

[![Offline AI](https://img.shields.io/badge/AI-Offline--Inference-teal?style=flat-square)](#)
[![VAPT Reporting](https://img.shields.io/badge/VAPT-Automated--Reporting-blue?style=flat-square)](#)
[![Privacy-Focused](https://img.shields.io/badge/Privacy-100%25--Local-success?style=flat-square)](#)

![VulnScribe Web UI Dashboard](/home/mint/.gemini/antigravity-ide/brain/ac68cfc1-4112-45de-b37c-639732576206/media__1786224229438.png)

---

## 1. The Problem

Manual VAPT reporting is tedious, repetitive, and time-consuming. It typically requires security engineers to:
* Constantly rewrite standard finding details (descriptions, CWE mappings, reference sheets).
* Spend hours formatting evidence paragraphs and screenshots.
* Manually research and draft impact statements and remediation steps.
* Manage raw PoC files and structure them cleanly into tables.
* Keep document layouts, headers, and color-coded severities consistent.

**VulnScribe automates the VAPT reporting workflow, drastically reducing reporting overhead so security testers can focus their time and energy on active technical testing.**

---

## 2. What VulnScribe Does

VulnScribe streamlines the document creation workflow by letting the AI handle structured formatting:

```
Tester
  ↓
Finding Details
  ↓
Observation + Severity
  ↓
PoC / Evidence Folder
  ↓
Offline AI
  ↓
Structured Finding
  ↓
Professional Report
```

---

## 3. Key Features

* **Local / Offline AI Processing**: Zero-leakage inference using quantized open-weights models running completely locally via Ollama.
* **PoC / Evidence Handling**: Automated merging and alignment of testing outputs and screenshots directly inside findings sections.
* **Automated Finding Documentation**: Generates fully completed descriptions, impacts, recommendations, references, and CWE/OWASP mappings.
* **Severity-Aware Reporting**: Color-coded layouts, native graphs, and CVSS Suggestions mapped to the finding threat level.
* **Professional Report Generation**: Produces styled Microsoft Word (`.docx`) documents with vertical centering, fixed widths, and clean alignments.
* **Custom Report Templates**: Ingests your firm's historical reports (`REPORT.md` / Python final configs) to match existing layouts.
* **No External AI API Required**: Runs entirely inside air-gapped target environments without leaking customer data.

---

## 4. How It Works

### Execution Flow
```
 1. Tester Creates Finding
         │
         ▼
 2. Input Observation Details
         │
         ▼
 3. Select Finding Severity
         │
         ▼
 4. Attach PoC/Evidence Folder (auto fetch PoC images)
         │
         ▼
 5. VulnScribe Processes Inputs (Hybrid TF-IDF Search)
         │
         ▼
 6. Local AI Generates Structured Content
         │
         ▼
 7. Final DOCX/PDF/HTML Report Compiled & Exported
```

> [!NOTE]
> **The tester provides the technical truth. AI handles the documentation formatting.**

### Detailed Step-by-Step Mechanism
1. **Tester Input**: The security analyst enters minimal details into the dashboard: the finding name (e.g. "Stored XSS") and the observation details.
2. **Context Retrieval**: The python backend tokenizes the finding title and performs a TF-IDF keyword match against `knowledge_base.json` (compiled from past report template data).
3. **Database Check**: If a match is found with a similarity score of >= 0.35, the tool retrieves the pre-approved enterprise writing template to guarantee consistency. If score is < 0.35, it triggers local LLM generation.
4. **AI Generation**: For low-similarity findings, the prompt is formatted with structured examples and sent to the local `deepseek-coder:1.3b` instance to output correct description, impact, and recommendations.
5. **Output**: The output is compiled in clean markdown and presented on the live dashboard for immediate editing or copy-to-clipboard actions.

---

## 5. Screenshots

### Web UI Dashboard
![Web UI Dashboard](file:///home/mint/.gemini/antigravity-ide/brain/ac68cfc1-4112-45de-b37c-639732576206/media__1786224229438.png)
*Capturing raw finding names, observations, and severity selections in a responsive interface.*

### Ingested Database Viewer
*Real-time rendering of all 27+ historical report templates that can be loaded with one click.*

### AI-Generated Preview
*Polished markdown output dividing technical impacts, recommendations, and CWE/OWASP categories.*

---

## 6. Before vs After

### Without VulnScribe
```
  Observation ──> Manual Writing ──> Manual Formatting ──> Copy Evidence ──> References ──> Repeat × 30 Findings
```

### With VulnScribe
```
  Observation + Severity + Evidence ──> VulnScribe ──> Structured Formatted Finding ──> Final VAPT Report
```

---

## 7. Privacy / Offline Architecture

```
                 VULNSCRIBE ENGINE
             ┌─────────────────────────┐
             │    Local Application    │
             │                         │
  Evidence ─>│ ──> Local AI (Ollama)   │  
             │ ──> TF-IDF Database     │
             │ ──> Document Compiler   │
             └─────────────────────────┘
                          X
                   External AI API
                  (Zero Data Leakage)
```

**All sensitive client assessment data, observations, IP addresses, and custom endpoints remain entirely inside the auditor's local environment.**

---

## 8. App Architecture

### Software Layers
```
      TypeScript / Tailwind CSS Web Dashboard
                         │
                         ▼
        FastAPI Local Python Controller
                         │
        ┌────────────────┴────────────────┐
        ▼                                 ▼
  TF-IDF Retrieval                  Local LLM via Ollama
  (knowledge_base.json)             (deepseek-coder:1.3b)
        │                                 │
        └────────────────┬────────────────┘
                         ▼
             OOXML Word Doc Generator
```

### Deep Architectural Details
* **Frontend Controller**: A React SPA styled using Tailwind v4.0. It coordinates browser state, queries the REST API, parses raw markdown structure on the client side, and displays real-time similarity metrics.
* **FastAPI Backend Server**: Running locally on `127.0.0.1:8000`. Acts as the coordinator between the filesystem database cache (`knowledge_base.json`), the Ollama HTTP sockets, and the DOCX OOXML parsing engines.
* **Semantic Retrieval Core**: Computes a Term Frequency-Inverse Document Frequency (TF-IDF) representation of all template findings. Employs cosine similarity matching to identify past reports containing similar observations.

---

## 9. Demo Walkthrough

The demo workflow demonstrates:
1. Entering raw observation inputs for a `Missing Rate Limiting` vulnerability.
2. Clicking **Generate** to search the local database for historical examples.
3. Automatically running the offline local model to compile the descriptions.
4. Viewing the refined markdown details (Impact, Recommendation, References, CWE, OWASP, CVSS suggestions).
5. Copying the generated output directly to clipboard.

---

## 10. Sample Generated Report Finding

### Impact
Absence of effective rate limiting allows an attacker to perform automated authentication attempts at scale. This significantly increases the feasibility of brute-force and credential-stuffing attacks, potentially resulting in unauthorized account access if weak or reused credentials are present.

### Recommendation
* Implement server-side rate limiting on all authentication endpoints.
* Apply block rates based on combined IP addresses and user account thresholds.
* Implement progressive login delays and account lockout locks.

### References
* OWASP Authentication Cheat Sheet
* CWE-307: Improper Restriction of Excessive Authentication Attempts

### CWE
CWE-307 – Improper Restriction of Excessive Authentication Attempts

### OWASP Mapping
A07:2021 – Identification and Authentication Failures

### CVSS Suggestion
Score: 7.5 | Vector: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H

---

## 11. Technology Stack

* **Frontend**: React, TypeScript, Tailwind CSS v4.0, PostCSS.
* **Backend**: FastAPI (Python 3), Uvicorn.
* **Local LLM**: Ollama (`deepseek-coder:1.3b`).
* **Retrieval/Database**: TF-IDF keyword vectorizer, `knowledge_base.json` cache.
* **Document Compilation**: python-docx, native OOXML XML compiler.

---

## 12. Security Design

* **100% Local Inference**: Runs entirely offline; zero data is transmitted over the network.
* **No Cloud Telemetry**: Excludes any usage logging or external cloud communication.
* **Data Sanitization**: Secrets and private credentials are automatically stripped prior to report compilation.
* **Input-Output Validation**: Inputs are restricted to safe alphanumeric characters to prevent command injections.

---

## 13. Project Roadmap

* [x] Offline AI local processing
* [x] Contextual finding generation
* [x] Evidence / RAG database caching
* [x] Report formatting (fixed tables, Arial font, vertical centering)
* [ ] Advanced document layout editor
* [ ] Multi-format exporter (PDF, HTML)
* [ ] Multi-language report translations

---

## 14. Disclaimer

VulnScribe is designed for authorized security assessment, penetration testing, and VAPT compliance reporting workflows. Ensure appropriate authorization is obtained before executing audits.
