# 🌉 Local AI Bridge

> **"Bridging the brain of Qwen 2.5 to the elegance of Google Antigravity."**

Welcome to **Local AI Bridge**, a lightweight, containerized MCP (Model Context Protocol) gateway. This project allows the **Google Antigravity IDE** to communicate seamlessly with a local **Qwen 2.5** instance running on **LM Studio**.

Designed with Swiss-engineered precision 🇨🇭 for an Enterprise Architect's workflow, this bridge keeps your data local, your latency low, and your AI stack fully automated.

---

## 🚀 The Mission

Google Antigravity is a brilliant agentic IDE, but sometimes the task requires the specific touch of a local powerhouse like **Qwen 2.5**. This bridge translates MCP tool calls into OpenAI-compatible API requests for LM Studio, wrapped in a production-ready Docker vessel.

### 🛠 Tech Stack

- **The Brain:** Qwen 2.5 (via [LM Studio](https://lmstudio.ai/))
- **The Transport:** [FastMCP](https://github.com/modelcontextprotocol/python-sdk) (Python/SSE)
- **The Vessel:** Docker (hosted on `fredlamenace/local-ai-bridge`)
- **The Pipeline:** GitHub Actions with Dev/QA/Main environment isolation.

---

## 🏗 Architecture (The "EA" View)

### 1. Logical Architecture
```mermaid
graph TD
    subgraph Client
        IDE["Google (Antigravity)"]
    end
    
    subgraph Bridge["Local AI Bridge"]
        MCP["FastMCP Server (SSE)"]
        Trans["API Translator"]
    end
    
    subgraph Inference["Inference Engine"]
        LM["LM Studio"]
        Model["Qwen 2.5 Model"]
    end

    IDE -->|"1. MCP Tool Call (SSE)"| MCP
    MCP -->|"2. Process Request"| Trans
    Trans -->|"3. OpenAI API Request"| LM
    LM -->|"4. Run"| Model
    Model -->|"5. Response"| LM
    LM -->|"6. Chat Completion"| Trans
    Trans -->|"7. Tool Result (SSE)"| IDE
```

### 2. Physical Architecture
```mermaid
graph TD
    subgraph Workplace["Workstation (Windows / WSL2)"]
        IDE2["Antigravity IDE"]
        Docker["Docker Engine"]
        Container["local-ai-bridge Container"]
    end
    
    subgraph LocalNet["Local Network"]
        LMHost["LM Studio Host (192.168.100.101)"]
    end

    IDE2 -->|"HTTP (SSE) @ Port 8000"| Container
    Container -->|"HTTP (REST) @ Port 1234"| LMHost
```