# Portainer Deployment Guide for FreePilots Vault ًںگ³

A quick, beginner-friendly guide to deploying FreePilots on any machine running Portainer.

---

## 1. Create a New Stack in Portainer

1. Open your Portainer Web UI.
2. Select your environment (e.g. `local` or remote Kali/Ubuntu machine).
3. Click on **Stacks** in the left sidebar.
4. Click **+ Add stack**.
5. Name the stack: `freepilots`.

---

## 2. Paste the Docker Compose Configuration

In the **Web editor** window, paste the following:

```yaml
version: '3.8'

services:
  freepilots-vault:
    image: python:3.11-slim
    container_name: freepilots-vault
    restart: always
    ports:
      - "8107:8000"
    environment:
      - PUBLIC_URL=https://dash.aaam.sa
      - VAULT_TOKEN=freepilot_secret_token_2026
      - STORAGE_DIR=/data
    volumes:
      - freepilots_storage:/data
    command: >
      sh -c "apt-get update && apt-get install -y git ffmpeg curl &&
             git clone https://github.com/aamabdulrhman-sudo/freepilots.git /app &&
             cd /app/server &&
             pip install --no-cache-dir -r requirements.txt &&
             uvicorn app.main:app --host 0.0.0.0 --port 8000"

volumes:
  freepilots_storage:
    name: freepilots_storage
```

---

## 3. Deploy Stack

1. Click **Deploy the stack** at the bottom of the page.
2. Portainer will pull the base image, install dependencies, and start the FreePilots server.
3. Once running, access your vault at your configured Cloudflare domain or `http://<HOST_IP>:8107`.
