# drive-chat1

🤖 Drive Chat Assistant (AI + Google Drive Agent)

An AI-powered agentic system that lets you interact with your Google Drive through natural language.
Built with FastAPI, LangChain, LangGraph, and the Google Drive API.

You can chat with your Drive to:

📂 List files (e.g., “Show all files added in the last 3 months”)

📊 Search finance spreadsheets (Excel, Google Sheets, CSV with keywords like finance, p&l, financial)

🗑️ Delete PDFs uploaded today (with confirmation before deletion)

🔗 Get download links for files (direct export links for Sheets, Excel, PDFs, CSVs)

🏗️ System Architecture
flowchart TD
    U[User Query\n(Chat UI)] -->|Natural Language| A[LangChain Agent]
    A -->|Workflow Control| G[LangGraph]
    G -->|API Calls| D[Google Drive API]
    D -->|Files Metadata & Links| G
    G --> A
    A -->|Formatted Response\n(Download links, actions)| U


User Query: Example → “Fetch finance spreadsheets”

LangChain Agent: Interprets intent (list, search, delete).

LangGraph: Manages multi-step workflows (like confirm-before-delete).

Google Drive API: Provides metadata + file download/export links.

Response: AI returns structured, human-readable answers with links.

🚀 Features

Conversational AI Interface → Powered by LangChain + LangGraph.

Agentic Decision Making → AI interprets your query, decides whether to call Drive APIs.

File Operations:

List recent files

Find finance-related spreadsheets

Delete today’s PDFs (safe confirm flow)

Download Links → Every file comes with a ready-to-use download/export link.

CORS-ready API → Works smoothly with React/Next.js frontend.

🛠️ Tech Stack

Backend: FastAPI + LangChain + LangGraph

Frontend: React/Next.js (chat UI)

Auth & API: Google Drive API (OAuth 2.0)

AI Model: OpenAI GPT (via LangChain agent)

Middleware: CORS for localhost dev

📂 Project Structure
backend/
│── main.py              # FastAPI + AI agent endpoints
│── drive_utils.py       # Google Drive API utilities
│── agent.py             # LangChain/LangGraph agent logic
│── credentials.json     # OAuth client secrets (private)
│── token.pickle         # Saved Google login token
frontend/
│── pages/index.js       # Chat UI (React/Next.js)

💡 Usage Examples
1. Show files in last 3 months

User:

Show all files added to Drive over the last 3 months


Assistant:

Found 5 files in the last 3 months:

1. P&L_Template.pdf (application/pdf)
   Download: https://drive.google.com/uc?id=1abc123&export=download
2. Financial-statements.xlsx (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet)
   Download: https://drive.google.com/uc?id=2def456&export=download

   2. Fetch finance spreadsheets

User:

Fetch Excel files related to finance


Assistant:

Found 2 finance spreadsheets:

1. P&L_Template.xlsx (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet)
   Download: https://drive.google.com/uc?id=1ghi789&export=download

2. Financial-statements-template (application/vnd.google-apps.spreadsheet)
   Download: https://docs.google.com/spreadsheets/d/2xyz123/export?format=xlsx

   3. Delete PDFs uploaded today

User:

Delete the PDFs added to Drive today


Assistant:

I found 1 PDF(s) uploaded today:

1. P&L_Template.pdf (application/pdf)
   Download: https://drive.google.com/uc?id=1pdf123&export=download

Do you want me to delete them? (yes/no)

User:

yes


Assistant:

Deleted 1 PDF(s):

1. P&L_Template.pdf (application/pdf)

🔐 Security Notes

Keep credentials.json and token.pickle private.

Never commit them to GitHub.

Use environment variables for production.
