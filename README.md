# 🚀 Vysio – Public Feedback & Issue Tracker

[![TestFlight Beta](https://img.shields.io/badge/TestFlight-Join%20Beta-0A84FF?logo=apple&logoColor=white)](https://testflight.apple.com/join/6UZqZvdA)
[![Website](https://img.shields.io/badge/Website-vysio.app-111827?logo=safari&logoColor=white)](https://vysio.app)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](./LICENSE)

Welcome to the official community and feedback repository for **Vysio** — the native iPad developer workspace for VS Code, GitHub Codespaces, and remote dev environments.

[📱 Website](https://vysio.app) • [🧪 Join TestFlight Beta](https://testflight.apple.com/join/6UZqZvdA) • [💬 Report an Issue](https://github.com/vysio-app/vysio-feedback/issues)

---

## 💡 What is Vysio?

Vysio turns your iPad into a desktop-class cloud development machine.

### Key Features

- ⌨️ **Native iPadOS Keyboard Integration**  
  Intercepts Magic Keyboard shortcuts directly (e.g. `Cmd+W`, `Cmd+T`, `Cmd+P`) without browser tab collisions.

- 🔒 **Biometric Security**  
  Protect your sessions and tokens with Face ID, Touch ID, or device passcode via Apple Keychain.

- 🚀 **Codespaces & Remote IDE Support**  
  Connect to GitHub Codespaces, `code-server`, Gitpod, and custom remote dev endpoints.

- 📺 **Distraction-Free Fullscreen**  
  No browser chrome, no tab bar conflicts, no address bar overlays.

---

## 🛠️ How to Report Bugs & Request Features

Use this repository to share feedback and help shape Vysio:

- 🐛 **Bug reports** → [Open Bug Report](https://github.com/vysio-app/vysio-feedback/issues/new?template=bug_report.yml)
- ✨ **Feature requests** → [Request a Feature](https://github.com/vysio-app/vysio-feedback/issues/new?template=feature_request.yml)
- 🗺️ **Roadmap visibility** → Track milestones and upcoming releases in Issues and Discussions

Please check existing issues before creating a new one to avoid duplicates.

---

## 🗺️ Public Roadmap

Our current public roadmap is organized into three phases:

### Phase 1 — TestFlight Beta
- Core iPad native client UX
- GitHub auth + Codespaces launch flow
- Basic remote URL support (`code-server`, Gitpod)
- Keyboard shortcut reliability improvements
- Stability and crash reporting loops

### Phase 2 — App Store Launch
- Production hardening and performance tuning
- Improved onboarding and connection diagnostics
- Expanded compatibility matrix for remote providers
- Security UX polish (session lock, biometric prompts)

### Phase 3 — Advanced Extensions
- Enhanced editor integration hooks
- Multi-workspace quality-of-life features
- Deeper remote configuration options
- Community-prioritized power-user requests

> Priorities may shift based on beta feedback and platform constraints.

---

## ❓ FAQ & Troubleshooting

<details>
<summary><b>How do I connect my self-hosted code-server?</b></summary>

1. Ensure your `code-server` instance is reachable over **HTTPS**.
2. Copy the full URL (e.g. `https://dev.yourdomain.com`).
3. Open Vysio on iPad and paste the workspace URL.
4. Authenticate using your server’s configured auth/token flow.

For private home-lab setups, use:
- [Tailscale](https://tailscale.com) (recommended for private mesh VPN)
- Cloudflare Tunnel (to expose securely without port forwarding)

Companion resources: [`vysio-companion`](https://github.com/vysio-app/vysio-companion)

</details>

<details>
<summary><b>Are Magic Keyboard shortcuts supported?</b></summary>

Yes. Vysio captures keyboard events natively on iPadOS, so common VS Code bindings such as `Cmd+Shift+P`, `Cmd+B`, and `Cmd+W` work more consistently than browser-based workflows.

</details>

<details>
<summary><b>Codespaces won’t load or reconnect reliably. What should I check?</b></summary>

- Confirm your GitHub account has access to Codespaces.
- Verify network quality and disable restrictive VPN/proxy rules temporarily.
- Ensure your org policies allow Codespaces usage.
- Try reconnecting from a clean app session and re-auth if needed.
- Open a bug report with logs/screenshots and repro steps.

</details>

---

## 🤝 Community Guidelines

Please read [CONTRIBUTING.md](./CONTRIBUTING.md) before opening issues.

By participating, you agree to keep discussions respectful, constructive, and focused on improving the product for everyone.

---

## 📄 License

Unless otherwise stated, content in this repository is licensed under the [MIT License](./LICENSE).
