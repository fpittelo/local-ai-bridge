# GEMINI PROJECT CONTEXT
# Scope: Project Level (/mnt/g/My Drive/HOME/WORKSPACE/HOME/local-ai-bridge)

## 1. PROJECT OVERVIEW
* **Name:** Local AI Bridge
* **Mission:** A lightweight, containerized MCP gateway bridging Google Antigravity IDE to local Qwen 2.5 (via LM Studio).
* **Location:** Cheseaux-sur-Lausanne (Home Lab / Workstation).

## 2. TECH STACK & ARCHITECTURE
* **Inference:** Qwen 2.5 via LM Studio.
* **MCP Server:** FastMCP (Python/SSE) @ Port 8000.
* **Containerization:** Docker (`fredlamenace/local-ai-bridge`).
* **CI/CD:** GitHub Actions with environment isolation (`dev`, `qa`, `main`).
* **Deployment:** WSL2 / Docker Engine.

## 3. MANDATES & CONSTRAINTS
* **Git Operations:** ALL git actions (commits, branches, PRs, etc.) MUST be performed via the GitHub MCP tools. Do NOT use local `run_shell_command("git ...")`.
* **Environment Strategy:** Adhere to the branch-to-environment mapping (`dev` -> dev, `qa` -> qa, `main` -> main).
* **Secrets:** Never log or expose `LM_STUDIO_API_KEY`.

## 4. DOCUMENTATION STANDARDS
* **README.md:** Maintain Logical and Physical Mermaid diagrams.
* **Project.md:** Tracks configuration, CI/CD workflows, and deployment steps.

## 5. REPOSITORY STRUCTURE
```text
local-ai-bridge/
├── .github/workflows/ci-cd.yml
├── src/main.py
├── Dockerfile
└── requirements.txt
```
