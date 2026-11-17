# 🛡️ FreePilots (Sunnypilot + Private Dashcam Vault)

<div align="center">

![FreePilots Banner](https://img.shields.io/badge/FreePilots-Sunnypilot%20Fork-00E5FF?style=for-the-badge&logo=shield&logoColor=black)
[![Base: Sunnypilot](https://img.shields.io/badge/Base-Sunnypilot%20Master-FF6F00?style=for-the-badge&logo=openpilot&logoColor=white)](https://github.com/sunnyhaibin/sunnypilot)
[![Docker](https://img.shields.io/badge/Docker-Vault%20Server-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Mazda CX-9](https://img.shields.io/badge/Mazda%20CX--9%202021-Optimized-C00000?style=for-the-badge&logo=mazda&logoColor=white)](docs/MAZDA_CX9_GUIDE.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

**The Enhanced Sunnypilot Fork with Built-in Private Dashcam Vault, First-Time Admin Security, Bilingual (Arabic/English) UI, and Mazda CX-9 Optimization.**

**النسخة المطورة من فورك Sunnypilot والمدمج بها نظام الخزنة التخزينية الخاصة لحفظ تسجيلات الداش كام بخصوصية 100%، مع حماية حساب المدير، ودعم كامل للغة العربية، وتخصيص متقدم لمازدا CX-9.**

[English](#-english-documentation) • [العربية (الدليل العربي)](#-الدليل-العربي) • [Comparison / المقارنة](#-freepilots-vs-stock-sunnypilot-vs-openpilot) • [Mazda CX-9 Guide](docs/MAZDA_CX9_GUIDE.md)

</div>

---

## ⚖️ FreePilots vs. Stock Sunnypilot vs. openpilot
### ما الذي يميز هذا الفورك (FreePilots) عن فورك Sunnypilot الأصلي و openpilot الرسمي؟

| الميزة / Feature | openpilot الرسمي | فورك Sunnypilot الأصلي | 🛡️ فورك FreePilots (هذا المشروع) |
| :--- | :---: | :---: | :---: |
| **مكان حفظ الفيديوهات (Storage)** | سحابة Comma السحابية | سحابة Comma / SunnyLink | **خزنتك الخاصة محلياً على جهازك 100%** |
| **الاشتراك المالي (Cost)** | يتطلب Prime ($24/شهر) | يعتمد على السحابة | **مجاني بالكامل للأبد بدون اشتراكات** |
| **الخصوصية (Data Privacy)** | الفيديوهات تُرفع لسيرفرات بأمريكا | تُرفع لجهات خارجية | **مستحيل يخرج أي بايت لشركة خارجية** |
| **خيار تفعيل الخزنة بالشاشة** | ❌ غير متوفر | ❌ غير متوفر | **✅ مدمج بالشاشة (`Settings -> Toggles`)** |
| **حماية الخزنة بكلمة مرور** | ❌ لا يوجد | ❌ لا يوجد | **✅ معالج إعداد حساب مدير مشفر (Admin Setup)** |
| **لغة لوحة التحكم (Language)** | إنجليزي فقط | إنجليزي فقط | **✅ عربي بالكامل (RTL) + إنجليزي (LTR)** |
| **الربط برمز QR Code** | ❌ غير متوفر | ❌ غير متوفر | **✅ ربط فوري بكاميرا الكوما والجوال** |
| **توافق مازدا CX-9 2021** | عزم قياسي عام | عزم مخصص ومطور | **عزم مخصص ومطور + حفظ الفيديوهات** |
| **أداء القيادة الذاتية (ADAS)** | أساسي | متقدم جداً (عزم، سرعات، مسارات) | **مطابق لـ Sunnypilot بالكامل دون أي نقص** |

---

# 🇺🇸 English Documentation

## What is FreePilots?
**FreePilots** is an official fork of **Sunnypilot** designed to give Comma Four, Comma 3, and Comma 3X owners **100% control and ownership over their dashcam and driving recordings**.

By default, stock openpilot and community forks upload drive footage to external cloud servers. FreePilots modifies the native upload engine (`uploader.py`) and adds a persistent toggle in the device's Settings UI (`FreePilots Private Vault`), rerouting all raw high-definition video chunks (`fcamera.hevc`, `dcamera.hevc`) and telemetry (`rlog.zst`) directly to your own self-hosted private vault over an encrypted stream.

## Key Features Added in this Fork:
1. **Direct Stream to Private Vault:** All recordings bypass Comma cloud and go straight to your own server.
2. **On-Screen Settings Toggle:** Integrated natively into Sunnypilot's UI under `Settings -> Toggles`.
3. **First-Time Admin Setup Wizard (`/setup`):** The server requires the administrator to create a secure username and password upon first launch.
4. **Bilingual Web Dashboard:** Instant toggle between Arabic (RTL) and English (LTR), with persistent local preference.
5. **QR Code Pairing:** Pair your Comma device in seconds by scanning the vault's QR code.
6. **Mazda CX-9 (2021+) Optimized:** Full torque smoothing, steer-to-zero capabilities, and radar-matched longitudinal control.

---

## 🚀 Quick Installation Guide

### Step 1: Deploy the Vault Server (On your PC / Server / Portainer)

Deploy using Docker Compose in Portainer:

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
      sh -c "apt-get update && apt-get install -y --no-install-recommends ffmpeg curl &&
             mkdir -p /app/app/templates &&
             curl -sSL https://raw.githubusercontent.com/aamabdulrhman-sudo/freepilots/master/vault/requirements.txt -o /app/requirements.txt &&
             curl -sSL https://raw.githubusercontent.com/aamabdulrhman-sudo/freepilots/master/vault/app/auth.py -o /app/app/auth.py &&
             curl -sSL https://raw.githubusercontent.com/aamabdulrhman-sudo/freepilots/master/vault/app/main.py -o /app/app/main.py &&
             curl -sSL https://raw.githubusercontent.com/aamabdulrhman-sudo/freepilots/master/vault/app/storage.py -o /app/app/storage.py &&
             curl -sSL https://raw.githubusercontent.com/aamabdulrhman-sudo/freepilots/master/vault/app/templates/setup.html -o /app/app/templates/setup.html &&
             curl -sSL https://raw.githubusercontent.com/aamabdulrhman-sudo/freepilots/master/vault/app/templates/login.html -o /app/app/templates/login.html &&
             curl -sSL https://raw.githubusercontent.com/aamabdulrhman-sudo/freepilots/master/vault/app/templates/index.html -o /app/app/templates/index.html &&
             pip install --no-cache-dir -r /app/requirements.txt &&
             cd /app && uvicorn app.main:app --host 0.0.0.0 --port 8000"

volumes:
  freepilots_storage:
    name: freepilots_storage
```

Open your domain (e.g. `https://dash.aaam.sa`), create your admin user, and your vault is ready.

### Step 2: Install FreePilots on Your Comma Device (In Vehicle)

#### Switch to this fork via SSH:
```bash
ssh comma@<DEVICE_IP>
cd /data/openpilot
git remote set-url origin https://github.com/aamabdulrhman-sudo/freepilots.git
git fetch origin
git reset --hard origin/master
git clean -fd
sudo reboot
```

#### Activate the Vault:
- From the Comma screen: Navigate to `Settings` -> `Toggles` -> Enable **FreePilots Private Vault**.
- Or via SSH command:
  ```bash
  python3 -c "from openpilot.common.params import Params; p=Params(); p.put_bool('FreePilotsVaultEnabled', True); p.put('FreePilotsVaultUrl', 'https://dash.aaam.sa'); p.put('FreePilotsVaultToken', 'freepilot_secret_token_2026')"
  ```

---

# 🇸🇦 الدليل العربي التفصيلي

## ما هو FreePilots؟
**FreePilots** هو فورك رسمي مطور ومبني مباشرة على **Sunnypilot**، صُمم خصيصاً لملاك أجهزة **Comma Four** و **Comma 3/3X** ليمنحك **التحكم والملكية الكاملة 100% لتسجيلات الداش كام والقيادة**.

بدلاً من رفع المقاطع إلى خوادم شركة comma في أمريكا ودفع اشتراك Prime شهري، تم دمج محرك الخزنة الخاصة داخل شاشة ونظام Sunnypilot ليقوم الكوما بإرسال الفيديوهات مباشرة إلى **سيرفرك الخاص في منزلك** عبر اتصال مشفر وآمن.

---

## مميزات هذا الفورك الإضافية:
1. 🛡️ **خصوصية كاملة:** الفيديوهات لا تغادر شبكتك الشخصية ولا تذهب لأي طرف ثالث.
2. 🔒 **حماية وأمان السيرفر (Admin Account):** يطلب منك السيرفر عند أول تشغيل إنشاء حساب مدير بكلمة مرور مشفرة.
3. 🌐 **لوحة تحكم معربة بالكامل:** دعم التبديل السلس بين العربية (RTL) والإنجليزية (LTR).
4. ⚙️ **تفعيل مباشر من الشاشة:** خيار **FreePilots Private Vault** متاح رسمياً داخل إعدادات Sunnypilot بالشاشة.
5. 🚗 **تخصيص كامل لمازدا CX-9 2021:** عزم مقود سلس، توجيه حتى الصفر، وتحكم طولي متوافق مع رادار مازدا.

---

## خطوات التثبيت السريع

### 1. تشغيل السيرفر عبر Portainer:
انسخ كود الـ Docker Compose الموضح بالأعلى، وشغله في Portainer، ثم افتح رابطك (مثال: `https://dash.aaam.sa`). أنشئ حسابك وسيكون السيرفر جاهزاً فوراً.

### 2. التبديل إلى فورك FreePilots في سيارتك:
ادخل عبر SSH على جهاز الكوما:
```bash
cd /data/openpilot && \
git remote set-url origin https://github.com/aamabdulrhman-sudo/freepilots.git && \
git fetch origin && \
git reset --hard origin/master && \
git clean -fd && \
sudo reboot
```

ثم فعّل الخيار من الشاشة: `Settings` ➔ `Toggles` ➔ **FreePilots Private Vault** وعيّن رابطك.

---

## 📄 الترخيص (License)
هذا المشروع مفتوح المصدر بالكامل تحت رخصة **MIT License**. متاح للجميع للاستخدام والتعديل والتطوير.