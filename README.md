# 🧠 Dual-Agent ReAct System with LangGraph, Tavily, and Python REPL

This project implements a **dual-agent ReAct-style architecture** using [LangGraph](https://python.langchain.com/docs/langgraph/), integrating **Tavily Web Search** and a **Python Code Execution REPL** to collaboratively answer user queries and generate charts.

---

## 📌 Overview

The system features two intelligent agents:

- **🔍 Research Agent**: Uses real-time web search via `Tavily` to fetch data.
- **📊 Chart Generator Agent**: Uses `PythonREPL` to run Python code and generate visualizations like charts.

These agents interact using a ReAct-style loop, passing messages and invoking tools until a `FINAL ANSWER` is produced.

---

## 🔧 Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/SubhamIO/collaborative_multi_agent_system.git
cd react-chart-bot
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

**Key dependencies**:

- `langchain`
- `langchain-groq`
- `langgraph`
- `langchain-community`
- `langchain-experimental`
- `python-dotenv`
- `tavily-python`
- `matplotlib`
- `pandas`

### 3. Add Environment Variables

Create a `.env` file in the project root with the following content:

```env
GROQ_API_KEY=your_groq_api_key
TAVILY_API_KEY=your_tavily_api_key
```

---

## 🚀 How It Works

### Agents

- **Researcher**: Uses `tv_search` tool to search the web via Tavily.
- **Chart Generator**: Uses `python_repl_tool` to execute Python code for chart generation.

### Tools

#### 🔍 `tv_search(query: str)`

Searches for up-to-date information using Tavily's API and returns a formatted string of top results.

#### 🐍 `python_repl_tool(code: str)`

Executes Python code using LangChain's `PythonREPL` and returns the printed output or error message.

### Workflow

LangGraph's `StateGraph` manages execution with conditional routing logic:
- If tool calls exist → go to `call_tool` node
- If `FINAL ANSWER` is detected → end the loop
- Else → switch agents

---

## 🧩 System Architecture

<img src="https://github.com/SubhamIO/collaborative_multi_agent_system/blob/main/agent_workflow.png" alt="Alt text" title="Optional title">

---

## 🧪 Example Use Case

**Prompt:**

```
Find the top 10 countries by GDP and plot a bar chart.
```

**Flow:**
1. `Researcher` fetches real GDP data using Tavily.
2. `chart_generator` writes and executes Python code using `matplotlib`.
3. Final output includes the plot and concludes with `FINAL ANSWER`.

---

## 📁 File Structure

```
📦 react-chart-bot/
├── .env
├── main.py
├── README.md
└── requirements.txt
```

---

## ✅ Output Sample

```markdown
### ✅ Executed Python Code:
```python
import matplotlib.pyplot as plt
plt.bar(["USA", "China", "Japan"], [25000, 17000, 5000])
plt.xlabel("Country")
plt.ylabel("GDP (Billion USD)")
plt.show()
```

### 🖨️ Output:
[Chart appears here]
```

---

## 📜 Requirements

- Python ≥ 3.8
- Valid API keys for:
  - [Groq](https://console.groq.com/)
  - [Tavily](https://app.tavily.com/)

---

## 🤝 License

This project is licensed under the **MIT License**.

---

## 🙋‍♂️ Author

Developed by Subham Sarkar. Reach out for collaboration, feature improvements, or deployment help.
