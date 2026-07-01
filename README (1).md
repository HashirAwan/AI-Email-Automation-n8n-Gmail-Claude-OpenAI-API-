# 🤖 AI Email Auto-Responder
### Automated Gmail replies powered by Claude AI + n8n

![Workflow Status](https://img.shields.io/badge/status-active-brightgreen)
![n8n](https://img.shields.io/badge/built%20with-n8n-orange)
![Claude AI](https://img.shields.io/badge/AI-Claude%20Sonnet-blue)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📸 Demo

> **How to add your screenshots:**
> 1. Create a `screenshots/` folder in this repo
> 2. Add your images/GIFs and replace the filenames below
> 3. Delete this tip once done!

### Workflow in n8n
![n8n Workflow](screenshots/workflow-overview.png)

### Incoming email → AI reply in action
![Email Demo GIF](screenshots/demo.gif)

### AI-generated reply in Gmail
![Gmail Reply](screenshots/gmail-reply.png)

---

## 🚀 What It Does

This automation monitors your Gmail inbox and uses **Claude AI** to generate professional, context-aware replies — automatically. No more writing the same types of responses over and over.

**The workflow:**
1. 📥 Gmail Trigger detects a new incoming email
2. 🔍 Filters out sent/spam emails
3. 📝 Extracts sender, subject, and email body
4. 🧠 Sends email content to Claude AI to generate a smart reply
5. 📤 Sends the AI-generated reply back via Gmail
6. 📋 Logs activity for tracking

---

## 💡 Business Value

| Without Automation | With This Tool |
|---|---|
| Manually reading & replying to every email | AI handles routine replies instantly |
| 5–15 mins per email response | ~0 minutes — fully automated |
| Inconsistent tone & quality | Professional, consistent replies every time |
| Delayed responses hurt conversions | Instant replies improve customer experience |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| [n8n](https://n8n.io) | Workflow automation engine |
| [Claude API](https://anthropic.com) | AI reply generation |
| Gmail OAuth2 | Email reading & sending |

---

## ⚡ Quick Start

### Prerequisites
- [n8n](https://docs.n8n.io/getting-started/installation/) installed (local or cloud)
- A Gmail account
- A Claude API key from [console.anthropic.com](https://console.anthropic.com)

---

### Step 1 — Clone the Repository

```bash
git clone https://github.com/HashirAwan/ai-email-automation.git
cd ai-email-automation
```

---

### Step 2 — Set Up Environment Variables

```bash
cp .env.example .env
```

Open `.env` and add your **Claude API key**:

```env
ANTHROPIC_API_KEY=sk-ant-your-key-here
```

---

### Step 3 — Start n8n

```bash
npx n8n
```

Then open [http://localhost:5678](http://localhost:5678) in your browser.

---

### Step 4 — Connect Gmail

1. In n8n, go to **Credentials → New Credential**
2. Search for **Gmail OAuth2**
3. Follow the OAuth flow to connect your Gmail account
4. Name it exactly: `Gmail Account`

---

### Step 5 — Add Claude API Key

1. In n8n, go to **Credentials → New Credential**
2. Search for **Header Auth**
3. Set:
   - **Name:** `x-api-key`
   - **Value:** your Claude API key
4. Name it exactly: `Claude API Key`

---

### Step 6 — Import the Workflow

1. In n8n, click **Workflows → Import from file**
2. Select `workflow.json` from this repo
3. Click **Save**
4. Toggle the workflow to **Active**

---

## 🎛️ Customization

### Change the AI Prompt
In the **Generate AI Reply** node, edit the `system` prompt to match your tone:

```json
"system": "You are a professional email assistant for [YOUR BUSINESS]. 
Reply in a [formal/friendly/concise] tone. 
Always mention [your key info]. 
Sign off with 'Best regards,\nYour Name'."
```

### Filter Specific Senders
Add an **IF node** after the Gmail Trigger to only process emails from specific domains:
```
{{ $json.from.includes('@importantclient.com') }}
```

### Add a Human Review Step
Instead of auto-sending, route the AI reply to a **Slack or Telegram message** for your approval first — just replace the Gmail Send node with a Slack/Telegram node.

---

## 📁 Project Structure

```
ai-email-automation/
├── workflow.json           # n8n workflow (import this)
├── .env.example            # Environment variable template
├── .gitignore
├── screenshots/            # Add your demo images here
│   ├── workflow-overview.png
│   ├── gmail-reply.png
│   └── demo.gif
├── docs/
│   └── setup-guide.md     # Detailed setup walkthrough
└── README.md
```

---

## 🔒 Privacy & Security

- Your emails are processed locally via n8n (nothing stored externally)
- Only the email body is sent to Claude API for reply generation
- API keys are stored in n8n credentials vault, never in code
- `.env` is gitignored — never committed to GitHub

---

## 🗺️ Roadmap

- [ ] Slack notification before sending (human-in-the-loop mode)
- [ ] Smart categorization (support / sales / spam)
- [ ] Google Sheets logging for all processed emails
- [ ] Support for Outlook / IMAP inboxes
- [ ] Auto-labelling emails in Gmail after processing

---

## 🤝 Contributing

Pull requests welcome. For major changes, open an issue first.

---

## 📄 License

MIT — free to use, modify, and distribute.

---

## 👤 Author

**Awan Hashir**  
AI Automation Specialist | Helping businesses save time with intelligent automation  
[LinkedIn](https://linkedin.com/in/hashirawan) · [GitHub](https://github.com/HashirAwan)
