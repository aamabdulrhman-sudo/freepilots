# ًں›،ï¸ڈ FreePilots Vault

<div align="center">

![FreePilots Banner](https://img.shields.io/badge/FreePilots-Private%20Vault-00E5FF?style=for-the-badge&logo=shield&logoColor=black)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Sunnypilot](https://img.shields.io/badge/Sunnypilot-Compatible-FF6F00?style=for-the-badge&logo=openpilot&logoColor=white)](https://github.com/sunnyhaibin/sunnypilot)
[![Mazda CX-9](https://img.shields.io/badge/Mazda%20CX--9%202021-Optimized-C00000?style=for-the-badge&logo=mazda&logoColor=white)](docs/MAZDA_CX9_GUIDE.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

**A 100% Private, Self-Hosted Dashcam & Drive Archive Server for Sunnypilot and Comma 3 / 3X / Comma Four.**

**ظ†ط¸ط§ظ… ط³ط­ط§ط¨ظٹ ط°ط§طھظٹ ط§ظ„ط§ط³طھط¶ط§ظپط© ظ„ط­ظپط¸ طھط³ط¬ظٹظ„ط§طھ ط§ظ„ط¯ط§ط´ ظƒط§ظ… ظˆط§ظ„ظ‚ظٹط§ط¯ط© ط§ظ„ط®ط§طµط© ط¨ط¬ظ‡ط§ط² ط§ظ„ظƒظˆظ…ط§ ظپظˆط± ظˆظپظˆط±ظƒ Sunnypilot ط¨ط®طµظˆطµظٹط© ظƒط§ظ…ظ„ط© 100% ط¹ظ„ظ‰ ط¬ظ‡ط§ط²ظƒ ط§ظ„ط´ط®طµظٹ.**

[English](#-english-guide) â€¢ [ط§ظ„ط¹ط±ط¨ظٹط© (ط§ظ„ط¯ظ„ظٹظ„ ط§ظ„ط¹ط±ط¨ظٹ)](#-ط§ظ„ط¯ظ„ظٹظ„-ط§ظ„ط¹ط±ط¨ظٹ) â€¢ [Mazda CX-9 Guide](docs/MAZDA_CX9_GUIDE.md) â€¢ [Portainer Setup](docs/PORTAINER_GUIDE.md)

</div>

---

## ًں“‘ Table of Contents / ط¬ط¯ظˆظ„ ط§ظ„ظ…ط­طھظˆظٹط§طھ
- [English Guide](#-english-guide)
  - [Overview](#overview)
  - [Why FreePilots?](#why-freepilots)
  - [Architecture](#architecture)
  - [Requirements](#requirements)
  - [Quick Start: Server Deployment](#quick-start-server-deployment)
  - [Quick Start: Comma Device Pairing](#quick-start-comma-device-pairing)
  - [Mazda CX-9 (2021) Compatibility](#mazda-cx-9-2021-compatibility)
- [ط§ظ„ط¯ظ„ظٹظ„ ط§ظ„ط¹ط±ط¨ظٹ (Arabic Guide)](#-ط§ظ„ط¯ظ„ظٹظ„-ط§ظ„ط¹ط±ط¨ظٹ)
  - [ظ†ط¸ط±ط© ط¹ط§ظ…ط©](#ظ†ط¸ط±ط©-ط¹ط§ظ…ط©)
  - [ظ„ظ…ط§ط°ط§ FreePilotsطں](#ظ„ظ…ط§ط°ط§-freepilotsطں)
  - [ظ…طھط·ظ„ط¨ط§طھ ط§ظ„طھط´ط؛ظٹظ„](#ظ…طھط·ظ„ط¨ط§طھ-ط§ظ„طھط´ط؛ظٹظ„)
  - [ط®ط·ظˆط§طھ طھط«ط¨ظٹطھ ط§ظ„ط³ظٹط±ظپط± (Docker / Portainer)](#ط®ط·ظˆط§طھ-طھط«ط¨ظٹطھ-ط§ظ„ط³ظٹط±ظپط±)
  - [ط®ط·ظˆط§طھ ط±ط¨ط· ط¬ظ‡ط§ط² ط§ظ„ظƒظˆظ…ط§ ظپظˆط±](#ط®ط·ظˆط§طھ-ط±ط¨ط·-ط¬ظ‡ط§ط²-ط§ظ„ظƒظˆظ…ط§-ظپظˆط±)
  - [ظ…ظ„ط§ط­ط¸ط© ط®ط§طµط© ظ„ظ…ظ„ط§ظƒ ظ…ط§ط²ط¯ط§ CX-9 2021](#ظ…ظ„ط§ط­ط¸ط©-ط®ط§طµط©-ظ„ظ…ظ„ط§ظƒ-ظ…ط§ط²ط¯ط§-cx-9-2021)
- [Troubleshooting & FAQ](#-troubleshooting--faq)
- [License](#-license)

---

# ًں‡؛ًں‡¸ English Guide

## Overview
**FreePilots** bridges the gap between open-source autonomous driving and user privacy. By default, comma devices running openpilot or forks send telemetry and camera recordings to comma.ai's cloud servers. 

With **FreePilots**, all road camera segments (`fcamera.hevc`), driver-facing recordings (`dcamera.hevc`), and telemetry data (`rlog.zst`) are automatically streamed directly to **your own private server** whenever your vehicle connects to Wi-Fi or LTE. Zero bytes are shared with any 3rd party.

## Why FreePilots?
- ًں”’ **100% Private & Local:** All driving footage and timestamps are stored exclusively on your hard drive.
- ًں’¸ **No Monthly Subscriptions:** Avoid paying $24/month for Comma Prime just to retain your drive history.
- ًں“± **QR Code One-Click Pairing:** Simply point your phone to the Comma camera to pair your vault in seconds.
- ًںڑ— **Vehicle Tailored:** Fully optimized for **Mazda CX-9 (2021+)**, **CX-5**, and any vehicle running Sunnypilot.
- ًںŒگ **Cloudflare Tunnel Friendly:** Access your drive archive securely from anywhere in the world over HTTPS.

## Architecture
```
 [ Comma Four / 3X ]  (in vehicle)
        â”‚
        â–¼ (WiFi / LTE via Encrypted HTTPS)
 [ FreePilots Vault ]  (Docker on your Home Server / Kali / VPS)
        â”‚
        â”œâ”€â”€ ًں“‚ /data/storage (Raw HEVC & MP4 stitched video)
        â””â”€â”€ ًںŒگ Web UI (Play, Search, Download, and Share)
```

## Requirements
### Server Side:
- Any Linux, Windows, or macOS machine with **Docker** and **Docker Compose** (or **Portainer**).
- Public access via **Cloudflare Tunnel**, Tailscale, or Port Forwarding.

### Device Side:
- Comma 3, Comma 3X, or **Comma Four**.
- Running **Sunnypilot** (or upstream openpilot/FrogPilot).
- SSH access enabled.

---

## Quick Start: Server Deployment

### Method 1: Using Docker Compose
1. Clone this repository:
   ```bash
   git clone https://github.com/aamabdulrhman-sudo/freepilots.git
   cd freepilots
   ```
2. Copy and adjust your environment variables:
   ```bash
   cp .env.example .env
   ```
3. Start the server:
   ```bash
   docker compose up -d
   ```
4. Access the web dashboard at `http://localhost:8107` (or your Cloudflare domain).

### Method 2: Portainer (1-Click Deployment)
See our detailed [Portainer Deployment Guide](docs/PORTAINER_GUIDE.md).

---

## Quick Start: Comma Device Pairing

1. SSH into your Comma device (or use the device terminal):
   ```bash
   ssh comma@<COMMA_IP_ADDRESS>
   ```
2. Run the automated 1-line installer:
   ```bash
   curl -sSL https://raw.githubusercontent.com/aamabdulrhman-sudo/freepilots/main/device/install.sh | bash
   ```
3. Enter your FreePilots Server URL (e.g. `https://dash.aaam.sa`) and Vault Token when prompted.
4. Done! Every future drive will now sync privately to your server.

---

# ًں‡¸ًں‡¦ ط§ظ„ط¯ظ„ظٹظ„ ط§ظ„ط¹ط±ط¨ظٹ

## ظ†ط¸ط±ط© ط¹ط§ظ…ط©
ظ…ط´ط±ظˆط¹ **FreePilots** طµظڈظ…ظ… ظ„ط­ظ„ ظ…ط´ظƒظ„ط© ط®طµظˆطµظٹط© طھط³ط¬ظٹظ„ط§طھ ط§ظ„ط¯ط§ط´ ظƒط§ظ… ظ„ظ…ظ„ط§ظƒ ط£ط¬ظ‡ط²ط© **Comma Four** ظˆ **Comma 3/3X**.  
ظپظٹ ط§ظ„ظˆط¶ط¹ ط§ظ„ط§ظپطھط±ط§ط¶ظٹطŒ ظٹظ‚ظˆظ… ط¬ظ‡ط§ط² ط§ظ„ظƒظˆظ…ط§ ط¨ط±ظپط¹ ظ„ظ‚ط·ط§طھ ط§ظ„ظƒط§ظ…ظٹط±ط§ ظˆط§ظ„ط±ط­ظ„ط§طھ ط¥ظ„ظ‰ ط®ظˆط§ط¯ظ… ط´ط±ظƒط© comma.ai ط§ظ„ط³ط­ط§ط¨ظٹط© ظپظٹ ط£ظ…ط±ظٹظƒط§. ظ…ط¹ **FreePilots**طŒ طھطµط¨ط­ طھط³ط¬ظٹظ„ط§طھظƒ ظ…ظ„ظƒظƒ ظˆط­ط¯ظƒطŒ ط­ظٹط« ظٹطھظ… ظ†ظ‚ظ„ظ‡ط§ ظ…ط¨ط§ط´ط±ط© ظˆط¨ط´ظƒظ„ ظ…ط´ظپط± ط¥ظ„ظ‰ **ط³ظٹط±ظپط±ظƒ ط§ظ„ط®ط§طµ ظپظٹ ظ…ظ†ط²ظ„ظƒ ط£ظˆ ط¬ظ‡ط§ط²ظƒ** ط£ظˆظ„ ظ…ط§ طھطھطµظ„ ط¨ط§ظ„ظˆط§ظٹ ظپط§ظٹ ط£ظˆ ط§ظ„ط´ط±ظٹط­ط©.

## ظ„ظ…ط§ط°ط§ FreePilotsطں
1. ًں›،ï¸ڈ **ط®طµظˆطµظٹط© ظ…ط·ظ„ظ‚ط© 100%:** ظ„ط§ طھط®ط±ط¬ ط£ظٹ ظ„ظ‚ط·ط© ط£ظˆ ط¥ط­ط¯ط§ط«ظٹط§طھ ط®ط§ط±ط¬ ط¬ظ‡ط§ط²ظƒ ط§ظ„ط´ط®طµظٹ.
2. ًں’° **ط¨ط¯ظٹظ„ ظ…ط¬ط§ظ†ظٹ ظ„ط§ط´طھط±ط§ظƒ Comma Prime:** ظˆظپط± 24 ط¯ظˆظ„ط§ط± ط´ظ‡ط±ظٹط§ظ‹ ظˆط§ط­ظپط¸ ط£ط±ط´ظٹظپ ظپظٹط¯ظٹظˆظ‡ط§طھظƒ ظ„ط³ظ†ظˆط§طھ ط¨ط¯ظˆظ† ظ‚ظٹظˆط¯ ط³ط­ط§ط¨ظٹط©.
3. ًں“² **ط±ط¨ط· ظپظˆط±ظٹ ط¨ط§ظ„ظ€ QR Code:** ظˆط¬ظ‡ ط´ط§ط´ط© ط¬ظˆط§ظ„ظƒ ظ„ظƒط§ظ…ظٹط±ط§ ط§ظ„ظƒظˆظ…ط§ ظˆظٹطھظ… ط¥ط¹ط¯ط§ط¯ ط§ظ„ط±ط¨ط· ظپظٹ ط«ظˆط§ظ†ظچ.
4. ًںڑک **طھظˆط§ظپظ‚ ظ…ط«ط§ظ„ظٹ ظ…ط¹ ظ…ط§ط²ط¯ط§ CX-9 2021:** ظ…طµظ…ظ… ظ„ظٹط¹ظ…ظ„ ط¨ط³ظ„ط§ط³ط© ظ…ط¹ ظپظˆط±ظƒ **Sunnypilot** ط§ظ„ظ…ظپط¶ظ„ ظ„ظ…ظ„ط§ظƒ ظ…ط§ط²ط¯ط§.
5. ًںŒگ **ط¯ط¹ظ… ظƒط§ظ…ظ„ ظ„ظ†ظپظ‚ Cloudflare Tunnel:** ظٹظ…ظƒظ†ظƒ ط§ظ„ط¯ط®ظˆظ„ ط¹ظ„ظ‰ طھط³ط¬ظٹظ„ط§طھظƒ ظ…ظ† ط£ظٹ ظ…ظƒط§ظ† ظپظٹ ط§ظ„ط¹ط§ظ„ظ… ط¨ط±ط§ط¨ط· HTTPS ط¢ظ…ظ†.

---

## ظ…طھط·ظ„ط¨ط§طھ ط§ظ„طھط´ط؛ظٹظ„

### ط£ظˆظ„ط§ظ‹: ط·ط±ظپ ط§ظ„ط³ظٹط±ظپط± (ط¬ظ‡ط§ط² ط§ظ„ظƒظ…ط¨ظٹظˆطھط± / ط§ظ„ط³ظٹط±ظپط±):
* ط¬ظ‡ط§ط² ظٹط¹ظ…ظ„ ط¨ظ†ط¸ط§ظ… (Linux / Kali / Ubuntu / Windows / Mac).
* ط¨ط±ظ†ط§ظ…ط¬ **Docker** ط£ظˆ ظ„ظˆط­ط© طھط­ظƒظ… **Portainer**.
* ط±ط§ط¨ط· ظ†ظپظ‚ ط®ط§ط±ط¬ظٹ ظ…ط¬ط§ظ†ظٹ ظ…ط«ظ„ **Cloudflare Tunnel** ظ„طھطھظ…ظƒظ† ظ…ظ† ط§ظ„ظˆطµظˆظ„ ط¥ظ„ظٹظ‡ ظ…ظ† ط®ط§ط±ط¬ ط§ظ„ط¨ظٹطھ.

### ط«ط§ظ†ظٹط§ظ‹: ط·ط±ظپ ط¬ظ‡ط§ط² ط§ظ„ظƒظˆظ…ط§ (ط§ظ„ط³ظٹط§ط±ط©):
* ط¬ظ‡ط§ط² **Comma Four** ط£ظˆ Comma 3 / 3X.
* ظ…ط«ط¨طھ ط¹ظ„ظٹظ‡ ظپظˆط±ظƒ **Sunnypilot**.
* طھظپط¹ظٹظ„ ط®ظٹط§ط± ط§ظ„ظ€ SSH ظ…ظ† ط§ظ„ط¥ط¹ط¯ط§ط¯ط§طھ (`Settings` â‍” `Developer` â‍” `Enable SSH`).

---

## ط®ط·ظˆط§طھ طھط«ط¨ظٹطھ ط§ظ„ط³ظٹط±ظپط±

### ط¹ط¨ط± Portainer:
1. ط§ط¯ط®ظ„ ط¹ظ„ظ‰ ظ„ظˆط­ط© **Portainer** â‍” طھظˆط¬ظ‡ ط¥ظ„ظ‰ ظ‚ط³ظ… **Stacks** â‍” ط§ط¶ط؛ط· **Add stack**.
2. ط³ظ…ظ‘ ط§ظ„ظ€ Stack ط¨ط§ط³ظ…: `freepilots`.
3. ط§ظ„طµظ‚ ط§ظ„ظƒظˆط¯ ط§ظ„طھط§ظ„ظٹ ظپظٹ ظ…ط­ط±ط± ط§ظ„ظˆظٹط¨:

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
      # ط¶ط¹ ط±ط§ط¨ط· ظƒظ„ط§ظˆط¯ ظپظ„ظٹط± ط§ظ„ط®ط§طµ ط¨ظƒ ظ‡ظ†ط§
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
4. ط§ط¶ط؛ط· **Deploy the stack**.
5. ط§ظپطھط­ ظ…طھطµظپط­ظƒ ط¹ظ„ظ‰ ط§ظ„ط±ط§ط¨ط· (ظ…ط«ط§ظ„: `https://dash.aaam.sa`) ظˆط³طھط¬ط¯ ظˆط§ط¬ظ‡ط© ط§ظ„طھط­ظƒظ… ط£ظ…ط§ظ…ظƒ ظ…ط¨ط§ط´ط±ط©!

---

## ط®ط·ظˆط§طھ ط±ط¨ط· ط¬ظ‡ط§ط² ط§ظ„ظƒظˆظ…ط§ ظپظˆط±

ط¹ظ†ط¯ظ…ط§ طھظƒظˆظ† ط¨ط¬ط§ظ†ط¨ ط³ظٹط§ط±طھظƒ ظˆط§ظ„ظƒظˆظ…ط§ ظ…طھطµظ„ ط¨ظ†ظ‚ط·ط© ط§طھطµط§ظ„ ط¬ظˆط§ظ„ظƒ ط£ظˆ ظˆط§ظٹ ظپط§ظٹ ط§ظ„ط¨ظٹطھ:

1. ط§ط¯ط®ظ„ ط¹ظ„ظ‰ ط§ظ„ظƒظˆظ…ط§ ط¹ط¨ط± ط§ظ„ظ€ SSH:
   ```bash
   ssh comma@<IP_ط§ظ„ظƒظˆظ…ط§_ط­ظ‚ظƒ>
   ```
2. ظ†ظپظ‘ط° ط£ظ…ط± ط§ظ„طھط«ط¨ظٹطھ ط§ظ„طھظ„ظ‚ط§ط¦ظٹ ط§ظ„ط¨ط³ظٹط· (ط³ط·ط± ظˆط§ط­ط¯ ظپظ‚ط·):
   ```bash
   curl -sSL https://raw.githubusercontent.com/aamabdulrhman-sudo/freepilots/main/device/install.sh | bash
   ```
3. ط³ظٹط·ظ„ط¨ ظ…ظ†ظƒ ظƒطھط§ط¨ط© ط±ط§ط¨ط· ط§ظ„ط³ظٹط±ظپط± ط­ظ‚ظƒ (ظ…ط«ط§ظ„: `https://dash.aaam.sa`) ظˆط±ظ…ط² ط§ظ„ط£ظ…ط§ظ† (`VAULT_TOKEN`).
4. **ط§ظ†طھظ‡ظ‰!** ط§ظ„ط³ظƒط±ظٹط¨طھ ط³ظٹظ‚ظˆظ… طھظ„ظ‚ط§ط¦ظٹط§ظ‹ ط¨طھط´ط؛ظٹظ„ ط®ط¯ظ…ط© ط§ظ„ظ…ط²ط§ظ…ظ†ط© ظˆط­ط¸ط± ط³ظٹط±ظپط±ط§طھ ط´ط±ظƒط© comma ظ„ط¶ظ…ط§ظ† ط¹ط¯ظ… طھط³ط±ظٹط¨ ط£ظٹ ظ…ظ‚ط·ط¹ ظپظٹط¯ظٹظˆ.

---

## ظ…ظ„ط§ط­ط¸ط© ط®ط§طµط© ظ„ظ…ظ„ط§ظƒ ظ…ط§ط²ط¯ط§ CX-9 2021
ط³ظٹط§ط±ط§طھ ظ…ط§ط²ط¯ط§ CX-9 طھطھظ…ظٹط² ط¨ظ†ط¸ط§ظ… طھظˆط¬ظٹظ‡ ظپط±ظٹط¯ (EPS). ظپظˆط±ظƒ **Sunnypilot** ظ‡ظˆ ط§ظ„ط®ظٹط§ط± ط§ظ„ط°ظ‡ط¨ظٹ ظ„ظ‡ط°ظ‡ ط§ظ„ط³ظٹط§ط±ط© ظ„طھط­ظ‚ظٹظ‚ ظ‚ظٹط§ط¯ط© ط°ط§طھظٹط© ظ…ط³طھظ‚ط±ط© ظˆط³ظ„ط³ط© ط¨ط¯ظˆظ† ط§ظ‡طھط²ط§ط²ط§طھ.  
ط±ط§ط¬ط¹ ط¯ظ„ظٹظ„ظ†ط§ ط§ظ„ظ…ط®طµطµ ظ„ط¶ط¨ط· ط£ظپط¶ظ„ ط¥ط¹ط¯ط§ط¯ط§طھ ط§ظ„طھظˆط¬ظٹظ‡ ظˆط§ظ„ط³ط±ط¹ط© ظپظٹ:  
ًں‘‰ [ط¯ظ„ظٹظ„ ط¥ط¹ط¯ط§ط¯ط§طھ ظ…ط§ط²ط¯ط§ CX-9 ط§ظ„طھظپطµظٹظ„ظٹ](docs/MAZDA_CX9_GUIDE.md)

---

## ًں› ï¸ڈ Troubleshooting & FAQ

#### Q: How do I know files are syncing?
A: Check the device service logs via SSH:
```bash
journalctl -u freepilot.service -f
```
Or view the storage counter directly on your FreePilots web dashboard.

#### Q: Does FreePilots delete recordings from the Comma device?
A: By default, files remain on the Comma device until space is needed. You can pass `--delete-after-upload y` during installation if you prefer immediate cleanup.

---

## ًں“„ License
This project is open-source under the **MIT License**. Free to use, modify, and distribute.
