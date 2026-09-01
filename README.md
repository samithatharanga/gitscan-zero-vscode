<div align="center">

  <img src="icon.svg" alt="GitScan-Zero Logo" width="100" height="100" />

  # GitScan-Zero for Visual Studio Code
  ### 🛡️ Air-Gapped, Zero-Cloud Real-Time Secret & Credential Leak Interceptor

  [![Visual Studio Marketplace Version](https://img.shields.io/visual-studio-marketplace/v/samithatharanga.gitscan-zero?style=for-the-badge&color=0284c7&label=Marketplace)](https://marketplace.visualstudio.com/items?itemName=samithatharanga.gitscan-zero)
  [![Visual Studio Marketplace Installs](https://img.shields.io/visual-studio-marketplace/i/samithatharanga.gitscan-zero?style=for-the-badge&color=38bdf8)](https://marketplace.visualstudio.com/items?itemName=samithatharanga.gitscan-zero)
  [![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)
  [![Open Source Security](https://img.shields.io/badge/Air--Gapped-100%25%20Local-blueviolet?style=for-the-badge)](#-privacy--architecture-blueprint)

  <p align="center">
    <b>Stop credential leaks at keystroke latency — before save, stage, or git commit.</b><br>
    Zero telemetry, zero external APIs, zero dependencies. 100% client-side memory execution.
  </p>

  <p align="center">
    <a href="https://marketplace.visualstudio.com/items?itemName=samithatharanga.gitscan-zero">Install from VS Code Marketplace</a> •
    <a href="#-why-gitscan-zero">Why GitScan-Zero</a> •
    <a href="#-quick-remediation-workflow">Quick Fixes</a> •
    <a href="#-detection-coverage-matrix">Detection Coverage</a>
  </p>

</div>

---

## 📌 Why GitScan-Zero?

Accidentally pushing production API keys, AWS credentials, or database tokens to GitHub or GitLab causes severe data breaches, API abuse, and cloud billing shock within minutes. 

Most conventional scanners run as post-commit hooks, CI/CD pipelines, or cloud-backed linters. By the time a CI/CD scanner flags a leak, the commit history may already be polluted. Furthermore, cloud-assisted scanners introduce privacy concerns by uploading source code to third-party endpoints.

**GitScan-Zero solves this directly inside your editor buffer:**
* **Proactive Interception:** Highlights exposed credentials instantly as you type (live diagnostic buffer).
* **Zero-Cloud / Air-Gapped:** Strictly processes AST tokens and regular expressions inside your local VS Code node process. No data ever leaves your computer.
* **Auto Remediation:** Fix vulnerable lines with a single shortcut (`Cmd + .` or `Ctrl + .`) to mask secrets, push values to `.env`, or suppress false positives.

---

## ✨ Key Features

* **⚡ Real-Time In-Memory Diagnostics:** Microsecond regex execution matches patterns instantly on code changes without bogging down editor performance.
* **🔒 100% Zero-Cloud Guarantee:** Runs entirely air-gapped without HTTP clients, tracking pixels, or remote analytics.
* **🛠️ Automated Quick Fixes:** Instant CodeActions to replace exposed values with placeholder masks or migrate keys to `.env` variables safely.
* **📁 Auto `.gitignore` Sync:** Verifies whether `.env` and sensitive environment configurations are tracked or ignored to prevent inadvertent git adds.
* **🛡️ Low False-Positive Rate:** Intelligent heuristic boundaries filter common sample/dummy strings (`123456`, `test-key`, `placeholder`).

---

## 🎯 Detection Coverage Matrix

GitScan-Zero continuously monitors active buffers for high-entropy tokens and signature patterns:

| Provider / Target | Pattern Description | Severity |
| :--- | :--- | :--- |
| **AWS Cloud** | Access Key IDs (`AKIA...`), Secret Keys | `Critical` |
| **OpenAI / Anthropic** | `sk-proj-...`, `sk-ant-...` API tokens | `Critical` |
| **GitHub** | Personal Access Tokens (`ghp_...`), Fine-grained Tokens (`github_pat_...`) | `High` |
| **Stripe** | Live Secret Keys (`sk_live_...`), Restricted Keys (`rk_live_...`) | `Critical` |
| **Google Cloud / Firebase** | Cloud API Keys (`AIza...`) | `High` |
| **Slack / Discord** | Webhooks and Bot Auth Tokens | `High` |
| **Private Keys & PKCS** | `-----BEGIN RSA/OPENSSH PRIVATE KEY-----` | `Blocker` |
| **Generic Secrets** | High-entropy Bearer Tokens, JWT secrets, Hardcoded DB URIs | `Warning` |

---

## 🚀 Quick Remediation Workflow

When a secret is detected, GitScan-Zero highlights the exact token with a warning squiggly.

1. Hover over the detected token or press **`Cmd + .`** (macOS) / **`Ctrl + .`** (Windows/Linux).
2. Choose your automated action:
   * **`✨ Mask Secret with [REDACTED]`** – Instantly replaces the sensitive value with a sanitized placeholder.
   * **`📦 Move to .env variable`** – Auto-creates a parameterized `process.env.VAR_NAME` reference.
   * **`Suppress warning (Add // gitscan-ignore)`** – Appends an inline bypass tag for intentional test mocks.

---

## 🔒 Privacy & Architecture Blueprint

```text
       +---------------------------------------------+
       |            Active Document Buffer           |
       +---------------------------------------------+
                              |
                              v
       +---------------------------------------------+
       |          Local Regex AST Scanner            | <--- (Zero Network Calls / 100% RAM)
       +---------------------------------------------+
                              |
            +-----------------+-----------------+
            |                                   |
            v                                   v
+-------------------------------+   +-------------------------------+
|  VS Code Diagnostic Provider  |   |  CodeAction QuickFix Engine   |
| (Underlines secret in editor) |   | (Masks / Redacts / Syncs .env)|
+-------------------------------+   +-------------------------------+

```


GitScan-Zero requires zero special workspace permissions and contains no external runtime dependencies (dependencies: {} in package.json).

📦 Installation
From VS Code Marketplace:

Open VS Code.

Press Cmd + Shift + X (or Ctrl + Shift + X) to open Extensions.

Search for GitScan-Zero and click Install.

Via VS Code CLI:

Bash
code --install-extension samithatharanga.gitscan-zero
👨‍💻 Author & Maintainer
Samitha Tharanga Wijesinghe

Organization: ST Imagix

GitHub: @samithatharanga

LinkedIn: Samitha Tharanga Wijesinghe

💖 Support & Contributions
Contributions, bug reports, and pattern additions are welcome via GitHub Issues and Pull Requests. If GitScan-Zero protected your repository from leaking secrets, please consider giving it a ⭐ star or supporting development through GitHub Sponsors.

📄 License
Licensed under the MIT License. Free for personal, commercial, and enterprise developer use.
