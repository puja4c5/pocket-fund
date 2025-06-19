# pocket-fund
AI powered company fact sheet generator using n8n
This repository contains an intelligent automation workflow built in n8n to streamline research, data enrichment, and reporting for companies. It simulates a real-world AI-powered research assistant that reads from a knowledge base (Google Sheets), performs conditional logic, conducts web research, generates insights using LLMs (like Gemini/OpenRouter).

✅ Built as part of the PocketFund AI Engineer Internship Assignment
📹 Watch Loom Demo Video 

📌 Project Objective
Design a complete, production-grade workflow that:

Accepts a company name via a webhook (input form).

Checks a Google Sheet (internal knowledge base) for existing data.

If the company is not found, performs web scraping + AI summarization.

Generates a Fact Sheet summarizing company insights.

Appends the sheet with the new entry.

🛠 Tools & Technologies Used
Tool	Role
n8n	, logic, automation engine
Google Sheets	Internal company database (Knowledge Base)
Serper API	External web search
OpenRouter / Gemini	LLMs used to generate summaries
Memory (Langchain)	Stores state between steps (for agents)

📋 Workflow Description
➤ Trigger:
Webhook (e.g., via a form like Tally) receives companyName as a query param.

➤ Step 1: Internal Database Lookup (Google Sheets)
Searches for the company in a spreadsheet.

If found → retrieves Status & InternalNotes.

➤ Step 2: Conditional IF Node
If company exists → Skip web search, use internal data.

If company not found → Go to next step.

➤ Step 3: External Web Research
Uses Serper.dev to query Google.

Extracts top snippet from results.

Passes snippet + name to an LLM (Gemini/OpenRouter).

Generates:

Status: "Researched"

InternalNote: 1-line insight

➤ Step 4: Append to Google Sheet
Writes new row with CompanyName, Status, and InternalNote.

➤ Step 5: Generate Final Fact Sheet 
Uses Langchain AI Agent (with memory & tool usage).

Builds a clean report.

✅ Sample Input / Output
Webhook Input (GET)
{ "CompanyName": "Anthropic" }
Google Sheet Before


| CompanyName  | Status    | InternalNotes                   |
|--------------|-----------|----------------------------------|
| OpenAI       | Invested  | Led by Sam Altman, LLM leader   |
Generated Output


{
  "companyName": "Anthropic",
  "status": "Researched",
  "internalNote": "Anthropic is an AI safety startup founded by former OpenAI employees."
}


🧪 Demo Video
🎥 Click to Watch the Loom Demo
Demonstrates:

Webhook Input

New company vs. existing company flow

Google Sheet updated in real-time

Email received

📂 Credentials Required
🔐 1. Google Sheets OAuth
Needed for reading/writing internal database.

Setup:

Google Cloud Console → OAuth Credentials

Enable Sheets API

Add n8n.cloud as redirect URI if hosted

OAuth setup from Google Cloud Console

🔐 3. Serper API Key
Register at https://serper.dev

Free plan available

Used for scraping Google search results

🔐 4. OpenRouter API Key (optional)
Register at https://openrouter.ai

Needed if using OpenRouter LLM (e.g., gpt-3.5 etc.)

🔐 5. Google Gemini (PaLM) API Key 
Needed for using Gemini 1.5 via LangChain

Apply from Google AI Studio

📎 Project Links
📄 Google Sheet - Knowledge Base (Public)

📽️ Loom Video Demo

📦 pocket_fund.json → Contains the full exported workflow

✅ Final Notes
Error handling (timeouts, search fallback) is built in for robustness.

Professional prompt design ensures clarity & insight in summaries.

Modular structure: easy to swap out LLMs or data sources.

🧑‍💻 Author
Puja Tripura

Passionate about automation, AI, and building intelligent assistants
