Below is the complete configuration to set up the **Local AI Bridge** repository.

---

## 1. Project Directory Structure

Ensure your repository follows this layout so the Dockerfile and Action can find the files.

```text
local-ai-bridge/
├── .github/
│   └── workflows/
│       └── ci-cd.yml    <- The automation engine
├── src/
│   └── main.py          <- The Python bridge script
├── Dockerfile           <- The container definition
└── requirements.txt     <- dependencies (fastmcp, httpx)

```

---

## 2. GitHub Environments & Secrets

Before pushing code, you must create three Environments in your GitHub repository settings (**Settings > Environments**): `dev`, `qa`, and `main`.

In **each** environment, add the following **Secret**:

* `LM_STUDIO_HOST`: (e.g., `http://192.168.100.101:1234`)
* `LM_STUDIO_API_KEY`: (Your xxxxxxxxxxxxxx key)

In your **Repository Secrets** (Global), add:

* `DOCKERHUB_USERNAME`: `fredlamenace`
* `DOCKERHUB_TOKEN`: (Generated from Docker Hub Settings > Security)

---

## 3. The CI/CD Workflow (`ci-cd.yml`)

This workflow triggers on pushes to your three branches. It dynamically selects the GitHub Environment based on the branch name.

```yaml
name: CI/CD Local AI Bridge

on:
  push:
    branches: [ "dev", "qa", "main" ]

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    # Dynamically select environment based on branch name
    environment: ${{ github.ref_name }}

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Build and Push
        uses: docker/build-push-action@v6
        with:
          context: .
          push: true
          # Tags the image with the branch name (e.g., fredlamenace/local-ai-bridge:dev)
          tags: |
            fredlamenace/local-ai-bridge:${{ github.ref_name }}
            ${{ github.ref_name == 'main' && 'fredlamenace/local-ai-bridge:latest' || '' }}
          build-args: |
            LM_HOST=${{ secrets.LM_STUDIO_HOST }}
            LM_KEY=${{ secrets.LM_STUDIO_API_KEY }}

```

---

## 4. The Optimized Dockerfile

This version utilizes `ENV` variables that can be overridden at runtime but are baked in with defaults from your GitHub Secrets during the build.

```dockerfile
FROM python:3.12-slim

WORKDIR /app

# Prevent Python from writing pyc files and buffering stdout
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY src/main.py .

# These are the default values from your CI/CD secrets
ARG LM_HOST
ARG LM_KEY
ENV LM_STUDIO_HOST=$LM_HOST
ENV LM_STUDIO_API_KEY=$LM_KEY

EXPOSE 8000

CMD ["python", "main.py"]

```

---

## 5. Deployment Recommendation

Since you are in **Cheseaux-sur-Lausanne** and likely running this on a home server or workstation:

1. **Pull the image:** `docker pull fredlamenace/local-ai-bridge:main`
2. **Run it:** ```bash
docker run -d 
--name local-ai-bridge 
-p 8000:8000 
--restart always 
fredlamenace/local-ai-bridge:main
```

### Verification

Once the container is running, verify the MCP endpoint is alive by visiting `http://<DOCKER_HOST_IP>:8000/sse` in your browser. You should see a "Server-Sent Events" stream or a connection message.