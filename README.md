# 🚀 Automated Lead Management & Error Recovery System

An intelligent lead ingestion pipeline built with **n8n** that automates data entry, lead prioritization, and fail-safe error logging.


<img width="994" height="339" alt="Screenshot 2026-02-19 000742" src="https://github.com/user-attachments/assets/5dbff13d-4982-481c-9a73-7a46267dfb6a" />

---

## 📋 Project Overview
This workflow transforms raw webhook data into a structured lead management system. It categorizes leads based on budget, alerts sales teams in real-time, and ensures 100% data integrity through automated error-handling branches.

## 🛠️ Tech Stack
* **Orchestration:** n8n
* **Tunneling:** ngrok (local-to-web connectivity)
* **Database:** Google Sheets
* **Communication:** Slack API & Gmail API
* **Logic:** Conditional Branching (IF Nodes) & Error Trigger Paths

---

## 🏗️ Key Features

### 1. Secure Webhook Ingestion
Utilizes an **ngrok** tunnel to securely expose the local n8n instance to external triggers (e.g., PowerShell commands or web forms), turning a local webhook into a live, accessible URL.

### 2. Fail-Safe Architecture
Configured with **"On Error -> Continue"** logic. If the primary Google Sheet fails (e.g., `#ERROR!` in cells), the system automatically redirects the payload to a dedicated **Error Log sheet** to prevent any data loss.

### 3. Smart Categorization & Automation
* **High-Value (Budget > ₹50,000):** Automatically tagged as "Priority" with an immediate notification sent to the team via **Slack**.
* **Standard (Budget ≤ ₹50,000):** Tagged as "Normal" with an automated confirmation email triggered via **Gmail**.

### 4. Data Synchronization
Uses email-based lookups to update existing rows, ensuring a clean database without duplicate entries.

---

## ⚙️ How It Works
1. **Trigger:** Data is posted to the n8n Webhook URL via the secure `ngrok-free.dev` tunnel.
2. **Backup:** The lead is immediately appended to a master Google Sheet.
3. **Error Check:** If the append fails, the error path catches the payload and logs details to a separate sheet.
4. **Logic Split:** An **IF Node** evaluates the `budget` field.
5. **Action:** The system updates the sheet status and triggers the appropriate communication channel (Slack or Gmail).

---

## 🔧 Setup & Installation

1. **Import Workflow:** Download the `.json` file from this repo and import it into your n8n instance.
2. **Establish Tunnel:** Start your ngrok tunnel:
   ```bash
   ngrok http 5678
