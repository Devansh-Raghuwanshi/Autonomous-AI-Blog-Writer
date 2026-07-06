# Autonomous AI Blog Writer: A Stateful Planning Agent with LangGraph

An advanced, multi-agent AI system built with LangGraph that autonomously plans, researches, writes, and formats comprehensive technical blogs. Unlike standard LLM wrappers that jump straight to generating text (often leading to generic or hallucinated content), this system employs a **Planning Agent architecture**. It breaks down complex topics, conducts live web research, executes parallel section writing, and dynamically generates contextual images.

Developed by **Devansh Singh Raghuwanshi**, this project demonstrates advanced capabilities in Agentic AI engineering, stateful multi-actor workflows, and Python backend development.

## ⚙️ Tech Stack
* **Orchestration:** LangChain & LangGraph (for complex, stateful multi-agent routing)
* **LLMs:** OpenAI / Local Open-Source Models (for routing, planning, and writing)
* **Image Generation:** Google Gemini API (for contextual diagram/image generation)
* **Web Search Tool:** Tavily API (Search engine optimized for LLMs)
* **Language & Data Validation:** Python, Pydantic (Strict structured outputs)

## 🧠 System Architecture & Workflow

The system is built on a Directed Acyclic Graph (DAG) architecture containing specialized nodes:

1. **Intelligent Router Node:** Evaluates the user's topic and categorizes it as *Closed-book* (evergreen, no research needed), *Open-book* (highly volatile, requires heavy research), or *Hybrid*. If research is required, it autonomously generates optimal search queries.
2. **Research Node:** Integrates with the Tavily API to fetch real-time web context. It deduplicates and packages the raw data into structured `Evidence` objects.
3. **Orchestrator (Planner) Node:** Analyzes the topic and the researched evidence to generate a highly detailed, section-by-section execution plan using Pydantic schemas (defining target word counts, tone, audience, and required resources per section).
4. **Parallel Worker Nodes (Fan-Out):** The graph dynamically fans out into multiple worker agents. Each worker independently and concurrently writes a specific section of the blog, dramatically reducing total generation time.
5. **Reducer Subgraph:** - **Merge Content:** Stitches the parallelly generated sections into a cohesive Markdown document.
   - **Decide Images:** An LLM reviews the full text to intelligently identify where visual aids (diagrams, tables, images) are needed and generates precise image prompts.
   - **Generate & Place:** Calls the Gemini API to create the images, saves them locally, and embeds the file paths directly into the final Markdown.

## 🚀 Setup & Installation

**1. Clone the repository**
\`\`\`bash
git clone https://github.com/yourusername/agentic-blog-writer.git
cd agentic-blog-writer
\`\`\`

**2. Create a virtual environment and install dependencies**
\`\`\`bash
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
pip install -r requirements.txt
\`\`\`

**3. Configure Environment Variables**
Create a `.env` file in the root directory and add your API keys:
\`\`\`env
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
GEMINI_API_KEY=your_google_gemini_api_key
\`\`\`

## ✨ Future Enhancements
* **Human-in-the-loop (HITL):** Adding a pause state after the Orchestrator node to allow user approval or modification of the blog plan before the workers start writing.
* **Custom Knowledge Base Integration:** Connecting the Research node to a local PostgreSQL/Vector database to write highly specific, proprietary company blogs.

---
*This repository showcases production-ready AI development, prioritizing structured outputs, parallel processing, and autonomous task delegation.*