# 🚀 AI Job Alert Organizer & Relevance Filter

AI-powered job alert management workflow built with **n8n**, **Groq Llama 3.1**, **Gmail API**, and **Google Sheets**.
Automatically fetches job alert emails, extracts details, deduplicates listings, scores against your target role, stores in a tracker, and sends a daily shortlist digest with application reminders.

---

![n8n](https://img.shields.io/badge/Built%20with-n8n-orange)
![Groq](https://img.shields.io/badge/LLM-Groq-green)
![Gmail](https://img.shields.io/badge/Email-Gmail-red)
![Google Sheets](https://img.shields.io/badge/Tracker-Google%20Sheets-green)
![License](https://img.shields.io/badge/license-MIT-blue)

---

## 📌 Problem Statement

Job alerts from multiple platforms become impossible to track in one place.
Important opportunities get buried under irrelevant listings, duplicates, and noise.

This workflow solves that by automatically:
- Fetching job alert emails from Gmail
- Extracting structured job details using AI
- Removing duplicate listings
- Scoring each job against your target role and skills
- Storing ranked opportunities in Google Sheets
- Sending a daily shortlist digest
- Sending application reminders for ignored opportunities

Result:
**Less noise → Better opportunities → Faster applications**

---

## 🚀 Features

✔ Auto-fetch job alert emails from Gmail  
✔ AI-powered job detail extraction  
✔ Duplicate job removal  
✔ AI resume match scoring  
✔ Opportunity priority calculation  
✔ Google Sheets job tracker  
✔ Daily shortlist digest email  
✔ Application reminder after 48 hours  
✔ Fit score + opportunity score ranking  

---

## 🏗 Workflow Architecture

```text
Schedule Trigger
        ↓
Fetch Job Alert Emails (Gmail)
        ↓
Extract Job Details (Groq Llama 3.3 70B)
        ↓
Remove Duplicate Jobs
        ↓
AI Resume Match Scorer (Groq Llama 3.1 8B)
        ↓
Calculate Opportunity Priority
        ↓
Store Opportunity Tracker (Google Sheets)
        ↓
Generate Daily Top Opportunities
        ↓
Send Daily Opportunity Digest (Gmail)
        ↓
Wait 48 Hours
        ↓
Check Application Status
        ↓
Send Application Reminder (Gmail)
```

---

## 🧠 AI Scoring System

### Fit Score
AI evaluates job against your target role and skills:

```json
{
  "fit_score": 85,
  "reason": "Strong match for AI Engineer role",
  "recommended": "YES"
}
```

### Opportunity Score Formula

```text
opportunity_score = (fit_score × 0.7) + (urgency_score × 0.3)
```

### Urgency Score

| Condition | Score |
|-----------|-------|
| Deadline exists | 90 |
| No deadline | 50 |

---

## 📊 Google Sheets Tracker Structure

Create a sheet named:

```text
Job Opportunities Tracker
```

Required columns:

| Column | Purpose |
|--------|---------|
| job_title | Extracted job role |
| company | Company name |
| location | Job location |
| salary | Package if mentioned |
| fit_score | AI match score |
| urgency_score | Deadline-based urgency |
| opportunity_score | Final priority score |
| recommended | YES / NO |
| reason | AI reasoning |
| apply_link | Application URL |
| Applied | YES / NO |
| Interview | YES / NO |
| Status | NEW / IN PROGRESS / CLOSED |
| Created_At | Timestamp |

---

## 📩 Email Outputs

### 1. Daily Shortlist Digest

Sent every cycle with top opportunities:

```text
🚀 Top Opportunity

Role: AI Engineer
Company: TechCorp
Location: Hyderabad
Salary: ₹12 LPA

AI Match Score: 87/100
Priority Score: 76/100

Recommendation: YES

Why this matters:
Strong Python and LLM skills match

Next Step: APPLY NOW
```

### 2. Application Reminder

Sent after 48 hours if Applied = NO:

```text
⏰ Reminder: Pending Job Application

You shortlisted this opportunity but have not applied yet.

Role: AI Engineer
Company: TechCorp
Opportunity Score: 76/100

Recommended action: Apply within 24–48 hours if still interested.
```

---

## ⚙ Tech Stack

| Tool | Purpose |
|------|---------|
| n8n | Workflow orchestration |
| Groq Llama 3.3 70B | Job detail extraction |
| Groq Llama 3.1 8B | Resume match scoring |
| Gmail API | Fetch emails + send digest |
| Google Sheets | Job opportunity tracker |
| JavaScript | Deduplication + scoring logic |

---

## 📦 Repository Structure

```text
.
├── workflow/
│     job-alert-organizer-workflow.json
│
├── screenshots/
│     workflow-overview.png
│     daily-digest-email.png
│     google-sheets-tracker.png
│
├── .env.example
├── .gitignore
└── README.md
```

---

## 🔧 Prerequisites

- n8n instance running
- Gmail OAuth configured
- Groq API key
- Google Sheets OAuth configured
- Job alert emails arriving in Gmail

---

## 🚀 Installation

Clone repository:

```bash
git clone https://github.com/your-username/ai-job-alert-organizer-n8n.git
cd ai-job-alert-organizer-n8n
```

Create env:

```bash
cp .env.example .env
```

Fill credentials:

```env
GMAIL_CREDENTIAL_ID=
GROQ_CREDENTIAL_ID=
GOOGLE_SHEETS_CREDENTIAL_ID=
GOOGLE_SHEET_DOCUMENT_ID=
SHEET_NAME=
YOUR_EMAIL=
YOUR_JOB_ALERT_EMAIL=
N8N_INSTANCE_ID=
```

Import workflow:
1. Open n8n
2. Workflows → Import
3. Select `workflow/job-alert-organizer-workflow.json`
4. Reconnect credentials
5. Set your Google Sheet ID and sheet name
6. Activate workflow

---

## ⚠️ Known Limitations

**Wait node** is set to 1 minute for testing purposes.
In production, change to 48 hours:

```text
Wait node → Amount: 48 → Unit: Hours
```

**Application status** requires manual update in Google Sheets:

```text
Applied = YES
```

to stop reminders. Future version will detect Gmail replies automatically.

---

## 🔒 Security

Never commit:
- Real Gmail credential IDs
- Groq API keys
- Google Sheets OAuth IDs
- Google Sheet document IDs or URLs
- Personal email addresses

Use placeholders before pushing to GitHub.

---

## 🛣 Roadmap

- [ ] Automatic Gmail reply detection
- [ ] Slack job alerts
- [ ] Telegram digest
- [ ] Multi-platform job scraping
- [ ] Resume auto-tailoring
- [ ] Interview tracker
- [ ] Dashboard analytics
- [ ] WhatsApp reminders

---

## 👨‍💻 Author

**Jagadeesh S**

Built using:
n8n + Groq + Gmail API + Google Sheets + JavaScript

If you found this useful, consider starring ⭐ the repository.
