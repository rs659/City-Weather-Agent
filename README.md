# 🏙️ City Weather and News Agent

An intelligent, interactive command-line AI agent powered by **LangChain**, **Groq**, and **Tavily**. This assistant answers city-specific queries by checking the current weather and pulling real-time local news. For enhanced safety and control, it includes a **Human-in-the-Loop (HITL) approval mechanism** that prompts you before any external tool is executed.

## 🚀 Features

- **🧠 Advanced LLM:** Uses the `qwen/qwen3.8-27b` model hosted on Groq for swift, context-aware reasoning.
- **🌦️ Real-time Weather:** Fetches live weather conditions and temperatures (metric) using the OpenWeather API.
- **📰 Local News Search:** Aggregates top recent news snippets and links about any city using Tavily Search.
- **🛡️ Human-in-the-Loop Middleware:** Intercepts agent tool requests and asks for explicit terminal approval (`yes/no`) before execution.
- **💻 Rich UI:** Utilizes the `rich` library for clean, visually appealing terminal console outputs.

---

## 🛠️ Prerequisites & Setup

### 1. Clone or Create the Project
Save your agent script as `main.py` in your working directory.

### 2. Install Dependencies
Install the required packages using `pip`:

```bash
pip install python-dotenv requests langchain-groq langchain-core tavily-python rich
```

### 3. Environment Variables Configuration
Create a `.env` file in the root directory of your project and populate it with your respective API keys:

```env
GROQ_API_KEY="your_groq_api_key_here"
OPENWEATHER_API_KEY="your_openweather_api_key_here"
TAVILY_API_KEY="your_tavily_api_key_here"
```

---

## 🕹️ How to Run

Launch the agent by executing the script in your terminal:

```bash
python main.py
```

### Example Usage Workflow

1. **Ask a question:** 
   ```text
   You : What's happening in Mumbai right now?
   ```
2. **Review & Approve the Tool Call:**
   ```text
   Agent wants to call 'get_news'. Approve? (yes/no): yes
   ```
3. **View Output:** The agent parses the approved tool results and displays a curated summary of current local updates.
4. **Exit:** Type `exit` at the prompt to end the session.

---

## 🧱 Code Architecture

- **`get_weather`**: Conversational LangChain tool linked to OpenWeatherMap API endpoints.
- **`get_news`**: Dynamic wrapper surrounding the Tavily Client search index.
- **`human_approval`**: A `@wrap_tool_call` middleware function injected into the agent runtime loop to enforce manual verification.
- **`create_agent`**: Builds the execution graph coordinating the tools, system prompt, and middleware array.
