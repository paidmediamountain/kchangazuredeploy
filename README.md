# KChang Azure Deploy — PyCharm Plugin

> Deploy and manage Azure Function Apps directly from PyCharm — no terminal switching required.

![Plugin Version](https://img.shields.io/badge/version-1.0.0-blue)
![PyCharm](https://img.shields.io/badge/PyCharm-2024.1%2B-green)
![License](https://img.shields.io/badge/license-Paid-gold)

---

## What Is This?

**KChang Azure Deploy** is a PyCharm plugin that brings the full Azure Function App workflow into your IDE. Write your Python function, hit Deploy, and it's live on Azure — without leaving PyCharm.

---

## Features

| Feature | Free | Pro |
|---|---|---|
| Azure Explorer tree — view all Function Apps | ✅ | ✅ |
| View Running / Stopped status | ✅ | ✅ |
| Open Function App in Browser | ✅ | ✅ |
| **One-click Deploy to Azure** | | ✅ |
| **Start / Stop / Restart Function Apps** | | ✅ |
| **Live Log Streaming** | | ✅ |
| **Edit Application Settings** | | ✅ |
| **Upload local.settings.json to Azure** | | ✅ |
| **Download Azure Settings to local.settings.json** | | ✅ |
| **Copy Function URL with Key** | | ✅ |
| **Create new Function Apps from PyCharm** | | ✅ |
| **Auto-fetch apps from Azure CLI** | | ✅ |

**Pro:** $9 one-time &nbsp;·&nbsp; or $5/month subscription &nbsp;·&nbsp; 30-day free trial included

---

## Requirements

- PyCharm 2024.1 or later (Community or Professional)
- [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) installed
- Logged into Azure CLI (`az login`)
- An active Azure subscription with at least one Function App

---

## Installation

### From JetBrains Marketplace (recommended)
1. Open PyCharm
2. Go to **Settings → Plugins → Marketplace**
3. Search for **KChang Azure Deploy**
4. Click **Install** → **Restart IDE**

### From Disk
1. Download the latest `.zip` from [Releases](../../releases)
2. In PyCharm: **Settings → Plugins → ⚙ → Install Plugin from Disk**
3. Select the downloaded `.zip` → **Restart IDE**

---

## Getting Started

### Step 1 — Install Azure CLI and Login
```bash
# Install Azure CLI (Windows)
winget install Microsoft.AzureCLI

# Login
az login
```

### Step 2 — Configure the Plugin
1. Open your Azure Function App project in PyCharm
2. Go to **Settings → Tools → Azure Function Deploy**
3. Click **Fetch from Azure CLI** to auto-fill your Subscription ID
4. Click **Fetch Apps from Azure** to select your Function App
5. Click **OK**

### Step 3 — Explore Your Function Apps
- Look for the **Azure Explorer** panel on the left sidebar
- Expand any Function App to see its **Functions** and **Application Settings**
- Right-click any app for a full context menu

### Step 4 — Deploy
- Go to **Tools → Deploy to Azure Function App...**
- Or right-click your app in the Azure Explorer → **Deploy...**
- Review the confirmation dialog → click **Deploy Now**
- Watch live output in the **Azure Deploy** panel at the bottom

---

## Usage Guide

### Azure Explorer
The **Azure Explorer** panel (left sidebar) shows all your Function Apps.

- 🟢 **Green** = Running
- ⚫ **Gray** = Stopped
- 🟠 **Orange** = Unknown state

**Expand any app** to see:
- **Functions** — all functions with their trigger types (httpTrigger, timerTrigger, etc.)
- **Application Settings** — key/value pairs (long values are masked for security)

**Right-click any app** for:

| Action | Description |
|---|---|
| Deploy... | Package and deploy your project to this app |
| Start | Start a stopped Function App |
| Stop | Stop a running Function App |
| Restart | Restart the Function App |
| Stream Logs... | Open a live log tab in the Azure Deploy panel |
| Edit Application Settings... | View and edit all settings in a table |
| Upload local.settings.json | Push local settings to Azure |
| Download Azure Settings | Save Azure settings to local.settings.json |
| Copy Function URL... | Get the invoke URL with function key |
| Open in Browser | Open the Function App URL in your browser |

---

### Deploying Your Function App

1. **Tools → Deploy to Azure Function App...**
2. Review the confirmation dialog showing your target app and settings
3. Click **Deploy Now**
4. The **Azure Deploy** panel opens at the bottom showing:
   - Packaging progress (which files are included)
   - Upload progress
   - Azure CLI output
   - ✅ SUCCESS or ❌ FAILED result

**Files excluded from deployment by default:**
```
.git, __pycache__, .venv, *.pyc, .env
```
You can customise exclude patterns in **Settings → Tools → Azure Function Deploy**.

---

### Live Log Streaming

1. Right-click any app in the Azure Explorer
2. Click **Stream Logs...**
3. A new tab opens in the **Azure Deploy** panel with live output
4. Click **Stop Streaming** to end the session

---

### Application Settings

**Edit in PyCharm:**
1. Right-click app → **Edit Application Settings...**
2. Add, edit, or remove key/value pairs
3. Click **OK** to save to Azure

**Upload from local.settings.json:**
1. Right-click app → **Upload local.settings.json to Azure...**
2. Confirm the number of settings to upload
3. Settings are pushed immediately to Azure

**Download to local.settings.json:**
1. Right-click app → **Download Azure Settings to local.settings.json...**
2. Confirm overwrite
3. File is saved to your project root

---

### Creating a New Function App

1. **Tools → Create Azure Function App...**
   Or click **+ New App** in the Azure Explorer toolbar
2. Fill in:
   - App Name (must be globally unique)
   - Resource Group
   - Region
   - Runtime (Python, Node, .NET, Java)
   - Runtime Version
   - Plan Type (Consumption / Premium / Dedicated)
3. Click **Create**
4. Progress is shown in the Azure Deploy panel

---

### Settings Reference

Go to **Settings → Tools → Azure Function Deploy**:

| Setting | Description |
|---|---|
| Subscription ID | Your Azure subscription (click Fetch to auto-fill) |
| Resource Group | The resource group containing your Function App |
| Function App Name | Target app for deployment |
| Region | Azure region (e.g. eastus, australiaeast) |
| Deployment Slot | Leave blank for production |
| Method | Azure CLI (recommended) |
| Source Directory | Leave blank to use project root |
| Exclude Patterns | Comma-separated patterns to skip during packaging |
| Restart after deploy | Restart the app after a successful deployment |
| Async deployment | Fire and forget — don't wait for deployment to complete |

---

## Troubleshooting

### "Azure CLI not found"
Install Azure CLI: https://docs.microsoft.com/cli/azure/install-azure-cli
Then restart PyCharm.

### "Not logged in to Azure"
Run `az login` in a terminal, then try again.

### "No function apps found"
Make sure your **Resource Group** is correct in settings, or leave it blank to list all apps across all resource groups.

### Deployment fails with 415 error
This is a known Azure CLI issue with some app configurations. The plugin automatically uses the stable `config-zip` deployment method which resolves this.

### Log streaming shows no output
Make sure **Application Logging** is enabled on your Function App:
Azure Portal → Your App → Monitoring → App Service Logs → Application Logging → On

---

## Contributing

Found a bug or have a feature request?
Open an issue at [github.com/kenchang/kchang-azure-deploy/issues](https://github.com/kenchang/kchang-azure-deploy/issues)

---

## Contact

**Ken Chang**
📧 paidmediamountain@gmail.com
🌐 [plugins.jetbrains.com](https://plugins.jetbrains.com)

---

## Changelog

### 1.0.0 — 2026-03-19
- Initial release
- Azure Explorer tree view
- One-click zip deployment via Azure CLI
- Start, Stop, Restart Function Apps
- Live log streaming
- Application Settings management
- Function browser with trigger types
- Copy Function URL with key
- Create new Function Apps from PyCharm
- Freemium model with 30-day free trial

---

*Not affiliated with Microsoft or JetBrains.*
