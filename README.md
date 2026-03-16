# 😄 Daily Joke Emailer — n8n Workflow

An automated workflow that fetches a random dad joke from a public API and sends it to your inbox every day. Built with n8n as Project 1 of a 30-day automation learning journey.

---

## 🔧 What It Does

1. Triggers manually (or on a schedule)
2. Calls the [icanhazdadjoke.com](https://icanhazdadjoke.com) free API
3. Extracts the joke text from the JSON response
4. Formats it into an email subject and body
5. Sends it to your Gmail inbox

---

## 🗺️ Workflow Structure

```
Manual Trigger → HTTP Request → Edit Fields → Gmail
```

| Node | Type | Purpose |
|------|------|---------|
| Manual Trigger | Trigger | Starts the workflow on demand |
| HTTP Request | Action | GET request to joke API |
| Edit Fields | Transform | Maps joke text to email fields |
| Gmail | Output | Sends the formatted email |

---

## ⚙️ Setup

### Prerequisites
- n8n installed locally (`npx n8n` or Docker)
- Gmail account with OAuth2 credentials configured
- Google Cloud project with Gmail API enabled

### Gmail OAuth2 Setup
1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a project → Enable Gmail API
3. Create OAuth2 credentials (Web application type)
4. Add redirect URI: `http://localhost:5678/rest/oauth2-credential/callback`
5. Paste Client ID + Secret into n8n Gmail credential

### Import the Workflow
1. Download `workflow.json` from this repo
2. Open n8n → Workflows → Import
3. Connect your Gmail credential
4. Hit **Execute Workflow**

---

## 🔑 Key Expressions Used

```
// Pull joke text from API response
{{ $json.joke }}

// Reference field from Edit Fields node
{{ $json.Subject }}
{{ $json.Body }}
```

---

## 📸 Output Example

**Subject:** Your daily joke 😄

**Body:** I broke my finger at work today. On the other hand, I'm completely fine.

---

## 🚀 Upgrade Ideas

- Replace Manual Trigger with **Schedule Trigger** (cron: `0 9 * * *`) to run every morning at 9am automatically
- Add an **IF node** to only send if `status == 200` (error handling)
- Swap joke API with **OpenAI** to generate a custom motivational quote instead
- Add **Google Sheets** logging to track which jokes were sent

---

## 🧠 What I Learned Building This

- How n8n's Trigger → Node → Output mental model works
- Making GET requests with the HTTP Request node
- Writing expressions with `{{ $json.fieldName }}` syntax
- Setting up Gmail OAuth2 credentials from scratch
- Reading the execution log to debug data flow
- Case sensitivity in field names (`Subject` ≠ `subject`)

---

## 🛠️ Tech Stack

- [n8n](https://n8n.io) — Workflow automation
- [icanhazdadjoke.com](https://icanhazdadjoke.com) — Free joke API (no auth needed)
- Gmail API — via Google OAuth2

---

## 📁 Files

```
├── README.md          ← You are here
└── workflow.json      ← Import this into n8n
```

---

## 🗓️ Part of My 30-Day n8n Learning Journey

This is Project 1 of 10 I'm building this month to become a professional automation developer.

| # | Project | Status |
|---|---------|--------|
| 1 | Daily Joke Emailer | ✅ Done |
| 2 | Google Sheets → Slack Lead Notifier | 🔄 Next |
| 3 | Daily Weather Briefing | ⏳ |
| 4 | Typeform → Airtable + Email | ⏳ |
| 5 | AI Email Auto-Responder | ⏳ |
| 6 | Multi-Channel Campaign Tracker | ⏳ |
| 7 | AI Content Calendar Engine | ⏳ |
| 8 | AI Lead Enrichment Pipeline | ⏳ |
| 9 | Customer Onboarding Automation | ⏳ |
| 10 | Competitor Intelligence Bot | ⏳ |

---

*Built by [@yourusername](https://github.com/yourusername) · Learning n8n automation in public*
