# 📖 Detailed Setup Guide

## Installing n8n

### Option A — Run Locally (Recommended for Testing)

```bash
# Install n8n globally
npm install n8n -g

# Start n8n
n8n start
```

Open http://localhost:5678

---

### Option B — Run with Docker (Recommended for Production)

```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  -e ANTHROPIC_API_KEY=your_key_here \
  n8nio/n8n
```

---

## Setting Up Gmail OAuth2

1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project (or use an existing one)
3. Enable the **Gmail API**
4. Go to **Credentials → Create Credentials → OAuth 2.0 Client ID**
5. Set application type to **Web Application**
6. Add `http://localhost:5678/rest/oauth2-credential/callback` as an authorized redirect URI
7. Download the credentials JSON
8. In n8n, create a Gmail OAuth2 credential using the Client ID and Client Secret

---

## Getting Your Claude API Key

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Sign up or log in
3. Navigate to **API Keys → Create Key**
4. Copy the key and add it to your `.env` file

---

## Testing the Workflow

1. Send yourself a test email
2. In n8n, open the workflow and click **Execute Workflow**
3. Check each node's output to verify data flows correctly
4. Check your Gmail Sent folder for the auto-reply

---

## Troubleshooting

| Problem | Fix |
|---|---|
| Gmail Trigger not firing | Make sure workflow is set to **Active** |
| Claude API returning 401 | Check your API key in n8n credentials |
| Emails sending to wrong thread | Verify `threadId` is being passed correctly |
| Rate limit errors | Add a **Wait** node (1–2 seconds) before the Claude API call |
