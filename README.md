<div align="center">

  <img src="assets/vysio-icon.png" alt="Vysio app icon" width="128" />

  # Vysio — Public Feedback & Issue Tracker

  **The developer browser for iPhone and iPad, with web tools and remote development built in.**

  [![Waitlist](https://img.shields.io/badge/Waitlist-Join%20Early%20Access-0A84FF?style=for-the-badge&logo=apple&logoColor=white)](https://vysio.app)
  [![Website](https://img.shields.io/badge/Website-vysio.app-111827?style=for-the-badge&logo=safari&logoColor=white)](https://vysio.app)
  [![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](./LICENSE)
  [![Twitter / X](https://img.shields.io/badge/X-%40vysio__app-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/vysio_app)

  <br />

  [📱 Website & Waitlist](https://vysio.app) • [🐛 Report a Bug](https://github.com/PierrePerrin/vysio.app.feedback/issues/new?template=bug_report.yml) • [✨ Request Feature](https://github.com/PierrePerrin/vysio.app.feedback/issues/new?template=feature_request.yml)

</div>

---

## 📸 Preview

<div align="center">
  <img src="assets/vysio-ipad-editor.png" alt="Vysio browser and remote development workspace on iPad" width="100%" style="border-radius: 12px; border: 1px solid rgba(255,255,255,0.1);" />
  <p><i>Vysio brings browsing and remote development tools together on iPad.</i></p>
</div>

---

## 💡 What is Vysio?

Vysio is a native browser for iPhone and iPad that brings everyday browsing and developer tools together.

### 🌟 Current App Features

- 🌐 **Desktop-class browsing** — Use a native tab strip, private tabs, Reader, bookmarks, history, and downloads.

- 🛠️ **Built-in Web Inspector** — Inspect and edit the DOM and CSS, and debug with console and network tools.

- 🧭 **Omnibar & Agent** — Navigate to sites and workspaces, run browser actions, summarize pages, compare tabs, and search browsing history.

- 💻 **Codespaces, code-server & SSH** — Manage GitHub Codespaces, connect to self-hosted `code-server`, and use SSH terminal tabs.

- 🔐 **Keychain & app lock** — Keep GitHub credentials in Apple Keychain and lock the app with Face ID, Touch ID, or your device passcode.

- ⌨️ **iPad workflows & iCloud sync** — Use Magic Keyboard shortcuts and multi-window on iPad; sync bookmarks and history through iCloud.

---

## 🛠️ How to Report Bugs & Request Features

Use this repository to share feedback and help shape the future of Vysio:

- 🐛 **Bug Reports** → [Open a Bug Report](https://github.com/PierrePerrin/vysio.app.feedback/issues/new?template=bug_report.yml)
- ✨ **Feature Requests** → [Suggest a Feature](https://github.com/PierrePerrin/vysio.app.feedback/issues/new?template=feature_request.yml)
- 🗺️ **Public Roadmap** → Track upcoming milestones in our Issues & Discussions

*Please search existing issues before opening a new one to prevent duplicates.*

---

## 🗺️ Public Roadmap

Our public roadmap is structured into three key milestones:

### 🔹 Phase 1 — TestFlight Beta (Current)
- [x] Core iPad native client UX & Magic Keyboard support
- [x] GitHub authentication & Codespaces launcher
- [x] Remote URL support (`code-server`, Gitpod)
- [ ] Keyboard shortcut customization & reliability fixes
- [ ] Beta feedback & crash reporting loops

### 🔹 Phase 2 — App Store Launch
- [ ] Production hardening & performance optimization
- [ ] Onboarding diagnostics for self-hosted instances
- [ ] Security polish (biometric session lock & auto-timeout)
- [ ] App Store release

### 🔹 Phase 3 — Advanced Extensions
- [ ] Multi-workspace switching & QoL enhancements
- [ ] Deep-link integrations (`vysio://workspace/...`)
- [ ] Advanced remote configuration hooks & community power features

---

## 📚 Blog & Setup Guides

Read our latest articles and technical guides directly in this repository:

- 🚀 [**Introducing Vysio**](./blog/en/introducing-vysio.md) — Why we built a native iPad client for cloud IDEs.
- ⌨️ [**Magic Keyboard & iPad Codespaces Setup**](./blog/en/magic-keyboard-ipad-codespaces-setup.md) — How to solve browser shortcut collisions.
- 📱 [**GitHub Codespaces on iPad Guide**](./blog/en/github-codespaces-ipad-guide.md) — Step-by-step mobile cloud dev workflow.
- 💡 [**Why We Built Vysio**](./blog/en/why-we-built-vysio.md) — The story behind desktop-class iPad dev tools.

*(Available in English `blog/en/` and French `blog/fr/`)*

---

## ❓ FAQ & Troubleshooting

<details>
<summary><b>How do I connect my self-hosted code-server?</b></summary>

1. Ensure your `code-server` instance is reachable over **HTTPS**.
2. Copy the full URL (e.g. `https://dev.yourdomain.com`).
3. Open Vysio on iPhone or iPad and paste the workspace URL.
4. Authenticate using your server’s configured auth/token flow.

For private home-lab setups, we recommend using:
- [Tailscale](https://tailscale.com) (private mesh VPN)
- Cloudflare Tunnel (secure public ingress)

See the [self-hosting templates](https://github.com/PierrePerrin/vysio.app.templates) for ready-to-deploy setups.

</details>

<details>
<summary><b>Are Magic Keyboard shortcuts supported?</b></summary>

Yes. Vysio captures keyboard events natively on iPadOS, so common VS Code bindings such as `Cmd+Shift+P`, `Cmd+B`, and `Cmd+W` work reliably without browser interception.

</details>

<details>
<summary><b>Codespaces won’t load or reconnect reliably. What should I check?</b></summary>

- Confirm your GitHub account has access to Codespaces.
- Verify network connectivity and temporarily disable restrictive VPN/proxy rules.
- Ensure your organization policies permit Codespaces usage.
- Open a bug report with logs, screenshots, and reproduction steps.

</details>

---

## 🤝 Community Guidelines

Please read [CONTRIBUTING.md](./CONTRIBUTING.md) before opening issues. Keep discussions respectful, constructive, and focused on improving Vysio.

---

## 📄 License

Content and documentation in this repository are licensed under the [MIT License](./LICENSE).
