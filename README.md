Automated Research Report Generator (n8n AI Agent Workflow)

An AI-powered workflow built on the n8n automation platform. Send a topic to a webhook, and an AI agent searches the web, reads articles, and returns a structured research report.

Student: Lalith Narayana Mogili
Student ID: 23085061
Course: Powers of AI (Saras Campus)
Assignment option: Option 2 - Automated Research Report Generator

How it works
A user calls the webhook with a topic, e.g. ?topic=Future of Electric Vehicles.
The AI Agent (powered by Google Gemini) searches for articles with the search_articles tool (Serper API).
It picks reliable sources (news sites, blogs, Wikipedia, tech sites) and skips social media and forums.
It reads the pages with the read_webpage tool and skips any that fail (timeout, forbidden, errors).
It analyzes the content and writes a report with a title, introduction, key insights, and conclusion.
Respond to Webhook returns the report as plain text in the browser.
Workflow nodes
Node	Purpose
Webhook	Receives the topic through a URL query parameter
AI Agent	Plans the steps, calls tools, and writes the report
Google Gemini Chat Model	Language model used for reasoning and text generation
search_articles	HTTP Request tool that calls the Serper API (Google search results)
read_webpage	HTTP Request tool that fetches webpage content
Respond to Webhook	Sends the finished report back to the caller
Setup
In n8n, create a new workflow and choose Import from file, then select workflow/research-report-workflow.json.
Open the search_articles node and replace YOUR_SERPER_API_KEY in the X-API-KEY header with your own key from serper.dev.
Open the Google Gemini Chat Model node and connect your own Google Gemini (PaLM) API credential.
Save the workflow and click Execute workflow (test mode), or activate it for the production URL.
Usage

Open this URL in a browser, using your own n8n host:

https://<your-n8n-host>/webhook-test/research-report?topic=Future of Electric Vehicles

Use /webhook/research-report instead once the workflow is active.

Example output

The response is plain text with a title, an introduction, key insights, and a conclusion. For the topic "Future of Electric Vehicles" it summarized market growth, new vehicle models, battery and charging advances, and environmental benefits.

Challenges and solutions
n8n server issues: platform-side outages affected execution (explained in the video).
API authentication: the Serper API key had to be sent in the HTTP headers.
Tool integration: each tool had to be connected as an AI Tool so the agent could call it.
Webpage access errors: the prompt tells the agent to skip failing pages and try other sources.
Prompt engineering: a clear step-by-step prompt keeps the agent working in the right order.
Future improvements
Save generated reports to Google Docs
Add more search APIs for better results
Improve webpage content extraction
Improve report formatting and structure
Repository structure
.
├── README.md
├── workflow/
│   └── research-report-workflow.json
├── docs/
│   └── AI_Agent_Workflow_Project_Report.pdf
└── screenshots/
    └── workflow.png
Links
Video demonstration: add your Google Drive link here
Project report: see docs/AI_Agent_Workflow_Project_Report.pdf
Security note

The workflow JSON in this repo has its API key removed. Never commit real API keys. Add your own keys locally in n8n.
