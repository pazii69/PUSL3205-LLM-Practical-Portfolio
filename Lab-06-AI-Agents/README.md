# 🎓 Intelligent University Assistant AI Agent

An AI-powered university assistant designed to help students with academic information, calculations, student records, schedules, and everyday university tasks.

The system uses a Python-based AI agent, an LLM, Retrieval-Augmented Generation (RAG), memory, and Google Workspace APIs to provide intelligent assistance.

## 🚀 Project Overview

The Intelligent University Assistant allows students to interact with an AI assistant that can answer university-related questions and use external tools to perform tasks.

The project demonstrates how Large Language Models (LLMs), AI agents, APIs, RAG, and automation can work together to create a practical university support system.

## ✨ Key Features

The project is designed around eight main capabilities:

| # | Feature | Description |
|---|---|---|
| 1 | Chat Interface | Allows students to communicate with the AI assistant. |
| 2 | AI Agent | Understands student requests and selects suitable tools. |
| 3 | University Information (RAG) | Retrieves relevant information from university documents and policies. |
| 4 | Google Calendar | Checks schedules and supports calendar event creation with approval. |
| 5 | Event Approval | Requests confirmation before creating calendar events. |
| 6 | Google Sheets | Searches and retrieves student records, with record updating planned. |
| 7 | Google Docs | Generates documents and reports. |
| 8 | Gmail | Sends emails and notifications with user approval. |

### Additional Capabilities

- Calculator tool for mathematical operations.
- SQLite-based conversation memory.
- University policy and information retrieval.
- Integration with Google Workspace services.

## 🛠️ Technologies Used

- **Python** – Main programming language.
- **Ollama** – Local Large Language Model runtime.
- **LangChain** – AI agent and tool integration.
- **SQLite** – Conversation memory storage.
- **RAG** – University document retrieval.
- **Google Calendar API** – Calendar integration.
- **Google Sheets API** – Student record access.
- **Google Docs API** – Document generation.
- **Gmail API** – Email notifications.
- **Kaggle Notebook** – Development and experimentation environment.

## 🏗️ System Architecture

```text
              Student
                 |
                 v
          Chat Interface
                 |
                 v
          Python AI Agent
                 |
          LLM (Ollama)
                 |
       Request Understanding
                 |
       +---------+---------+
       |         |         |
       v         v         v
      RAG      Memory   Calculator
       |
       v
  University Knowledge

       AI Agent Tools
             |
    +--------+--------+
    |        |        |
    v        v        v
 Calendar  Sheets   Google Docs
                      |
                      v
                    Gmail
```

## 📂 Project Structure

```text
Intelligent-University-Assistant/
│
├── README.md
├── Lab6_AIAgent.ipynb
├── requirements.txt
├── knowledge_base/
│   └── university_documents/
│
├── data/
│   └── student_records/
│
└── .gitignore
```

*Note: Update the filenames and folders above to match the actual files in your repository.*



## 🔐 Security

- Never upload Google OAuth client secrets.
- Never upload access tokens or refresh tokens.
- Never commit passwords, API keys, or private credentials.
- Use environment variables or a secure secrets manager.
- Obtain user approval before sending emails or creating calendar events.

## 📊 Development Status

| Component | Current Status |
|---|---|
| Python AI Agent Prototype | Developed |
| Calculator Tool | Tested |
| SQLite Conversation Memory | Tested |
| University RAG Search | Tested |
| Google Calendar Integration | Tested |
| Calendar Event Approval | Tested |
| Google Sheets Student Search | Tested |
| Google Docs Generation | Tested |
| Gmail Notifications | Tested |
| Calendar Availability Checking | Needs further implementation |
| Student Record Updating | Needs implementation |
| Unified Natural Language Tool Routing | Needs further implementation |
| Complete Chat Interface | Needs implementation |

The project is currently a working prototype with several individually tested integrations. The complete eight-feature assistant is still under development.

## 🎯 Project Objectives

- Develop a practical AI-powered university assistant.
- Explore the use of LLMs and AI agents.
- Implement Retrieval-Augmented Generation (RAG).
- Integrate external services using APIs.
- Demonstrate conversation memory.
- Improve student productivity through intelligent assistance.
- Explore secure, approval-based task execution.

## 🔮 Future Improvements

- Complete the unified conversational interface.
- Improve natural-language tool selection.
- Implement Google Sheets record updates.
- Add calendar free/busy availability checking.
- Improve document retrieval and response accuracy.
- Add better error handling and authentication management.
- Complete end-to-end testing of all eight capabilities.

## 👨‍💻 Author

**Project:** Intelligent University Assistant AI Agent

**Subject:** Large Language Models and Generative AI

**Development Environment:** Python / Kaggle

---

⭐ If you find this project interesting, feel free to explore the repository!
