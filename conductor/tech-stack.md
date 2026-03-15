# Tech Stack: Local AI Bridge

## Languages & Core Frameworks
- **Python 3.12:** The primary programming language for the bridge implementation.
- **FastMCP:** A high-level Python framework for building Model Context Protocol (MCP) servers with built-in support for SSE (Server-Sent Events).
- **HTTPX:** A fast, asynchronous HTTP client for Python, used to communicate with the LM Studio API.

## Inference & AI Models
- **Qwen 2.5:** The target large language model, running locally.
- **LM Studio:** The local inference platform providing an OpenAI-compatible API endpoint.

## Infrastructure & DevOps
- **Docker:** Containerization platform for consistent deployment across different environments.
- **GitHub Actions:** CI/CD orchestration for automated building, testing, and pushing images to Docker Hub.
- **GitHub Environments:** `dev`, `qa`, and `main` environments for lifecycle isolation.

## Host Environment
- **WSL 2 (Ubuntu):** The primary host environment for running the development and production containers on Windows 11.
- **Docker Engine:** The container runtime environment.
