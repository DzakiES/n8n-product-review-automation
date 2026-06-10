# 🤖 n8n Product Review Automation

An automated product review pipeline built with **n8n** and **Google Gemini AI**. This workflow automatically handles incoming customer feedback emails — classifying sentiment, requesting review permissions, and opening support tickets — with zero manual work after setup.

---

## 📌 What It Does

When a customer sends a feedback email, the workflow:

1. **Picks up the email** via IMAP trigger
2. **Analyzes the sentiment** using Google Gemini AI
3. **Branches into 3 paths** based on the result:
   - ✅ **Positive** → Sends a permission request email to use their feedback as a website review
   - 😐 **Neutral** → Does nothing, workflow stops
   - ❌ **Problem** → Automatically opens a support ticket on behalf of the customer

When the customer replies to the permission email:

4. **A second workflow** catches the reply
5. **AI classifies** the reply as YES or NO
6. **YES** → Opens a ticket to add the review to the website
7. **NO** → Does nothing

---

## 🔧 Tech Stack

| Tool | Purpose |
|---|---|
| [n8n](https://n8n.io) | Workflow automation |
| Google Gemini (via AI Agent node) | Email sentiment classification |
| Gmail / IMAP | Email trigger and sending |
| SupportCandy (WordPress) | Ticket creation |

---

## 📂 Files

| File | Description |
|---|---|
| `Product Review Automation.json` | Main n8n workflow — import this into your n8n instance |

---

## 🚀 How to Use

### 1. Import the workflow
- Open your n8n instance
- Go to **Workflows** → click **Import**
- Upload `Product Review Automation.json`

### 2. Set up credentials
You'll need to connect:
- **Gmail / IMAP** — your email account (use an App Password for Gmail)
- **Google Gemini** — get a free API key at [aistudio.google.com](https://aistudio.google.com)
- **SupportCandy** — your WordPress site URL + admin credentials

### 3. Configure the IMAP trigger
- Host: `imap.gmail.com`
- Port: `993`
- SSL: enabled
- Mailbox: `INBOX`

### 4. Activate the workflow
- Toggle the workflow to **Active**
- It will now run automatically on every new email

---

## 🧠 How the AI Classification Works

The AI Agent node uses this prompt logic:

- **POSITIVE** → happy/satisfied message, suitable as a product review
- **NEUTRAL** → neither positive nor negative, no action needed
- **PROBLEM** → complaint or issue, opens a support ticket

The prompt is designed to return **one word only**, which feeds directly into the Switch node for clean branching.

---

## 📄 License

MIT License — see [LICENSE](./LICENSE) for details.

---

Built by [Dzaki Endraghani Sunarko](https://github.com/DzakiES)
