 🤖 Agentic Research Assistant

> An AI-powered multi-agent research system that transforms a research question into a structured, evidence-based report through automated planning, multi-source search, source analysis, quality evaluation, and synthesis.

---

## 📌 Overview

The **Agentic Research Assistant** is a multi-agent AI system designed to automate the end-to-end research process.

Instead of relying on a single Large Language Model (LLM) to answer a question directly, the system divides the research process among multiple specialized agents.

Given a research question, the system:

1. 🧠 Breaks the question into focused research sub-questions
2. 🔎 Searches multiple information sources
3. 📖 Reads and normalizes retrieved sources
4. 🔍 Evaluates source quality and relevance
5. ✍️ Synthesizes the strongest information
6. 📄 Produces a structured research report with references

The goal is to create a more **structured, source-aware, and reliable research workflow** than a simple single-prompt LLM response.

---

# 🏗️ System Architecture

```text
                         👤 USER
                           │
                           │ Research Question
                           ▼
                    ┌───────────────┐
                    │ 🧠 PLANNER    │
                    │     AGENT     │
                    └───────┬───────┘
                            │
                            │ Research Sub-Questions
                            ▼
                    ┌───────────────┐
                    │ 🔎 SEARCHER   │
                    │     AGENT     │
                    └───────┬───────┘
                            │
                  ┌─────────┴─────────┐
                  ▼                   ▼
             🌐 Tavily             📚 arXiv
                  │                   │
                  └─────────┬─────────┘
                            ▼
                    ┌───────────────┐
                    │ 📖 READER     │
                    │     AGENT     │
                    └───────┬───────┘
                            │
                            ▼
                    ┌───────────────┐
                    │ 🔍 CRITIC     │
                    │     AGENT     │
                    └───────┬───────┘
                            │
                     Reliable Sources
                            │
                            ▼
                    ┌───────────────┐
                    │ ✍️ SYNTHESIZER│
                    │     AGENT     │
                    └───────┬───────┘
                            │
                            ▼
                    ┌───────────────┐
                    │ 📄 FINAL      │
                    │ RESEARCH      │
                    │ REPORT        │
                    └───────────────┘

🧠 Multi-Agent Workflow

The system consists of five specialized agents, with each agent responsible for a specific stage of the research pipeline.

1. 🧠 Planner Agent

The Planner receives the user's research question and decomposes it into several focused research sub-questions.

Example

Research Question:

How is artificial intelligence transforming healthcare?

The Planner may generate sub-questions covering areas such as:

Clinical and diagnostic applications
Economic and operational impact
Ethical, regulatory, and privacy considerations

This creates a structured research plan before information retrieval begins.

2. 🔎 Searcher Agent

The Searcher executes the research plan and retrieves relevant information from multiple sources.

The current implementation uses:

🌐 Tavily for web search
📚 arXiv for academic research papers

Search results from the generated sub-questions are collected and combined into a unified source set.

Using multiple source types allows the system to retrieve both:

General web-based information
Academic research literature
3. 📖 Reader Agent

The Reader processes and normalizes the retrieved sources so that downstream agents can work with a consistent representation.

It extracts and organizes information such as:

Source title
URL
Content
Source type
Research context
Relevant evidence

The normalized sources are then passed to the Critic for evaluation.

4. 🔍 Critic Agent

The Critic evaluates the retrieved sources before they are used for final synthesis.

Sources are assessed based on factors such as:

Relevance to the research question
Credibility
Evidence quality
Information usefulness
Research value

A hybrid evaluation approach is used to improve source selection and reduce dependence on weak or irrelevant sources.

5. ✍️ Synthesizer Agent

The Synthesizer receives the strongest evaluated sources and generates the final research report.

The final report is designed to:

Directly address the original research question
Combine information from multiple sources
Organize findings into meaningful sections
Avoid relying on a single source
Include references to supporting information
🔄 End-to-End Research Pipeline
                    User Question
                          │
                          ▼
                  🧠 Research Planning
                          │
                          ▼
                 Generate Sub-Questions
                          │
                          ▼
                  🔎 Multi-Source Search
                          │
                 ┌────────┴────────┐
                 ▼                 ▼
              Tavily             arXiv
                 │                 │
                 └────────┬────────┘
                          ▼
                  📚 Source Collection
                          │
                          ▼
                   📖 Source Reading
                          │
                          ▼
                🔍 Source Evaluation
                          │
                          ▼
                Reliable Source Selection
                          │
                          ▼
                  ✍️ Research Synthesis
                          │
                          ▼
                 📄 Final Research Report
💡 Example
Input
How is artificial intelligence transforming healthcare?
Processing
Planner
   ↓
Research Sub-Questions
   ↓
Tavily + arXiv
   ↓
Retrieved Sources
   ↓
Reader
   ↓
Critic
   ↓
Reliable Sources
   ↓
Synthesizer
Output

The system generates a structured research report covering the major aspects of the topic and provides references to the information used during synthesis.

✨ Key Features
🤖 Multi-agent AI architecture
🧠 Automated research planning
🔎 Multi-source web research
📚 Academic paper retrieval through arXiv
📖 Automated source processing and normalization
🔍 Source quality and relevance evaluation
🧩 Hybrid critic-based source filtering
✍️ LLM-powered research synthesis
📄 Structured research reports
🔗 Source references
🔐 Secure API key handling
🧱 Modular agent-based architecture
🛠️ Technology Stack
Technology	Purpose
🐍 Python	Core development
🧠 Large Language Models	Planning, evaluation, and synthesis
⚡ Groq	LLM inference
🔎 Tavily	Web search
📚 arXiv	Academic research retrieval
☁️ Google Colab	Development and experimentation
📓 Jupyter Notebook	Research workflow
🧩 Why a Multi-Agent Approach?

A traditional LLM-based research workflow often looks like:

Research Question
       ↓
      LLM
       ↓
     Answer

While this can be useful for general questions, it does not explicitly separate research planning, retrieval, source evaluation, and synthesis.

This project instead uses:

Research Question
       ↓
    Planning
       ↓
     Search
       ↓
     Reading
       ↓
   Evaluation
       ↓
    Selection
       ↓
    Synthesis
       ↓
     Report

Each stage has a dedicated responsibility.

This separation makes the research process more structured and allows retrieved information to be evaluated before it contributes to the final answer.

🚀 Getting Started
1. Clone the Repository
git clone https://github.com/YOUR_USERNAME/Agentic-Research-Assistant.git
cd Agentic-Research-Assistant
2. Install Dependencies
pip install -r requirements.txt
3. Configure API Keys

The project requires API keys for:

Groq
Tavily
Google Colab

The notebook can securely retrieve API keys using Google Colab Secrets:

from google.colab import userdata

GROQ_API_KEY = userdata.get("GROQ_API_KEY")
TAVILY_API_KEY = userdata.get("TAVILY_API_KEY")
⚠️ Security

Never hardcode API keys into the source code or commit them to GitHub.

Do not use:

GROQ_API_KEY = "your_actual_api_key"

Instead, use environment variables, Colab Secrets, or another secure secrets-management method.

▶️ Running the Project

The current implementation was developed and tested using Google Colab.

Steps
Open the project notebook.
Configure the required API keys.
Install the required dependencies.
Run the notebook cells in order.
Enter a research question.
Execute the research pipeline.
Review the generated research report and references.
📂 Project Structure
Agentic-Research-Assistant/
│
├── 📓 agentic_research_assistant.ipynb
├── 📄 README.md
├── 📦 requirements.txt
├── 🚫 .gitignore
│
└── 📁 src/
    ├── planner.py
    ├── searcher.py
    ├── reader.py
    ├── critic.py
    ├── synthesizer.py
    └── pipeline.py

The project is currently centered around the research notebook, with further modularization of the individual agents planned as the project evolves.

🔐 API Key Security

API keys are intentionally retrieved from secure environment-specific storage rather than being stored directly in the repository.

The repository should never contain:

GROQ_API_KEY=actual_secret_key
TAVILY_API_KEY=actual_secret_key

Before making the repository public, always verify that no credentials or secrets have been committed.

📊 Research Output

For a research question, the system produces a structured report based on the strongest sources identified during the research process.

The output can contain:

Research overview
Key findings
Supporting evidence
Synthesized conclusions
Source references
⚠️ Limitations

The quality of the final research report depends on several factors, including:

Quality of retrieved sources
Availability of external search services
LLM-generated planning and evaluation
API availability and usage limits
Accuracy and completeness of retrieved information

The system should therefore be treated as a research assistance tool, and information should be independently verified for high-stakes applications.

🔮 Future Improvements

Planned improvements include:

🌐 Streamlit or Gradio user interface
📑 PDF research report generation
🔗 Advanced citation verification
🧠 Persistent research memory
🗂️ Research history
🔎 Additional academic and web sources
📊 Advanced source ranking
📈 Confidence scoring
⚡ Parallel agent execution
☁️ Cloud deployment
🧪 Automated evaluation and benchmarking
📈 Project Status
Component	Status
🧠 Planner Agent	✅ Completed
🔎 Searcher Agent	✅ Completed
🌐 Tavily Integration	✅ Completed
📚 arXiv Integration	✅ Completed
📖 Reader Agent	✅ Completed
🔍 Critic Agent	✅ Completed
✍️ Synthesizer Agent	✅ Completed
📄 Final Research Report	✅ Completed
🔐 API Key Handling	✅ Completed
🌐 User Interface	🔮 Future Improvement
☁️ Cloud Deployment	🔮 Future Improvement
🎯 Learning Outcomes

This project demonstrates practical experience with:

Generative AI
Agentic AI systems
Multi-agent architecture
LLM orchestration
Information retrieval
Web search integration
Academic research retrieval
Source evaluation
Prompt engineering
Research synthesis
API integration
Secure secret management
Python-based AI application development
👩‍💻 Author
Sahithya Guttula

This project was developed as a Generative AI / Agentic AI project demonstrating how specialized AI agents can collaborate to automate a complete research workflow.

⭐ Support

If you find this project useful or interesting, consider giving the repository a ⭐ star!


### One important improvement I made

I changed the README so it **doesn't claim that the Streamlit UI is completed**. It is correctly listed under:

> 🔮 Future Improvements

That's important for your portfolio because the README should represent the actual state of the project.

I also removed unnecessary repetition and arranged the sections in a logical order:

**Overview → Architecture → Agents → Pipeline → Example → Features → Tech Stack → Why Multi-Agent → Setup → Running → Structure → Security → Output → Limitations → Future → Status → Learning Outcomes → Author**

That reads much more like a proper GitHub project than a notebook description.

**Next, I can build the exact `requirements.txt` from the libraries your working notebook actually uses**, so we don't accidentally miss a dependency or add unnecessary packages.
