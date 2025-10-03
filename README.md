# LinkedIn Post Approval Workflow (n8n)

## 📌 Overview
This repository contains an **n8n workflow** that automates the process of generating, reviewing, and publishing LinkedIn posts for a startup team.  
The workflow uses **AI (OpenAI)** to draft posts from weekly highlights, milestones, and reflections, and introduces a **review + approval system** with automated rejection handling.

---

## ⚙️ Features
- 📝 **AI Drafting**: Automatically generates LinkedIn posts using OpenAI (`gpt-4o-mini`) based on team input.
- 📋 **Form Trigger**: Collects highlights, milestones, and reflections via a form submission.
- 📧 **Approval via Email**: Sends draft posts to reviewers for quick approval or rejection.
- ✅ **Approval Path**:
  - Sends confirmation email.  
  - Publishes approved post directly to LinkedIn.  
-  **Rejection Path**:
  - Logs rejected posts into **Supabase**.  
  - Uses AI to rewrite and improve the post.  
  - Resubmits for approval automatically.  
- 🔄 **Retry Handling**:  
  - Retries up to **3 times** with rewritten posts.  
  - If rejected 3 times, notifies reviewer via email for **manual intervention**.

---

## 📂 Repository Structure
linkedin-post-approval-n8n/
│
├── README.md # Documentation for this workflow
└── workflows/
└── linkedin-post-approval.json # Exported n8n workflow

---

## 🔑 Setup

### 1. Prerequisites
- [n8n](https://n8n.io) installed (self-hosted or cloud).
- An **OpenAI API key**.
- **SMTP credentials** (for sending approval emails).
- **Supabase account** and table for logging rejections.
- **LinkedIn credentials** (person ID for the target account).

### 2. Import Workflow
- In n8n, go to **Workflows → Import from File**.
- Import the JSON file from `/workflows/linkedin-post-approval.json`.

### 3. Configure Environment
Replace placeholders in the workflow with your own details or move them into environment variables:

```env
OPENAI_API_KEY=your_openai_key
SMTP_FROM=your_sender_email@example.com
SMTP_TO=your_reviewer_email@example.com
LINKEDIN_PERSON_ID=your_linkedin_person_id
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_service_role_key
SUPABASE_TABLE=linkedin_post_logs
4. Run the Workflow
Submit the form trigger with your weekly update.
Workflow will draft a post → send for approval → auto-publish or retry if rejected.
🚀 Roadmap
 Add multi-person approval (e.g., require 2 reviewers).
 Add Slack or Teams integration for notifications.
 Add scheduling to post at specific times instead of immediately.
📝 License
This project is licensed under the MIT License.
🙌 Credits
n8n for automation.
OpenAI for natural language generation.
Supabase for logging and persistence.
LinkedIn API for publishing posts.
