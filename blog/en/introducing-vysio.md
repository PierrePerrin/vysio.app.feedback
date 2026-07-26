---
title: "Coding on iPad: running VS Code and GitHub Codespaces in a native client"
date: "2026-06-21"
description: "A practical look at why Safari gets in the way of Codespaces on iPad, and what Vysio does differently with shortcuts, screen wake, and credentials."
image: "/vysio-ipad-editor.png"
author: "Pierre Perrin"
readTime: "4 min read"
---

I kept trying to make the iPad work as a real coding machine. The hardware was never the problem: an M-series iPad, a good screen, a Magic Keyboard, and a cellular connection are more than enough when the actual compute runs somewhere else.

Cloud editors such as GitHub Codespaces, Gitpod, and self-hosted `code-server` instances should make that setup simple. In practice, the editor loads fine, and then the small browser problems start to pile up.

That is the gap **Vysio** is meant to close.

## Where Safari Gets in the Way

You can open `github.dev` or a `code-server` URL in Safari and get a familiar VS Code interface. The issue is not whether it loads. The issue is whether the iPad keeps behaving like a development machine after that.

### 1. Keyboard Shortcut Conflicts
The first problem is muscle memory. If you try to close an editor tab in VS Code with `Cmd + W`, Safari closes the browser tab. If you press `Cmd + P` to open the file picker, Safari opens the print dialog.

Those are not edge cases. They are shortcuts developers hit all day.

### 2. Screen Sleep and Connection Drops
Cloud containers need a steady connection. If the iPad display sleeps during a build or test run, Safari can lose the WebSocket connection. When you come back, you are waiting for the editor to reconnect instead of reading the result.

### 3. Credential Storage
To manage Codespaces properly, an app needs to hold GitHub OAuth credentials somewhere. Browser storage is not ideal for that job, and it can also be cleared by iOS under some conditions. The result is familiar: another sign-in flow at the exact moment you wanted to start working.

---

## What Vysio Does Differently

Vysio is a native iPad app built around a configured WebKit view, not a normal browser tab. The goal is narrow: make remote VS Code and Codespaces feel usable on iPad without sending your work through an extra backend.

### Native Keyboard Passthrough
Vysio configures its WebKit layer so common editor shortcuts reach the remote workspace. Commands like `Cmd + W`, `Cmd + N`, `Cmd + T`, and `Cmd + P` pass through to VS Code instead of being handled as browser commands.

### Screen Wake Lock
When a workspace is open, Vysio keeps the iPad awake. Long builds and test runs are much less likely to be interrupted by the device going idle.

### Tokens in Keychain
GitHub OAuth tokens are stored in the Apple Keychain, protected by Face ID, Touch ID, or your iPad passcode. Vysio talks directly to the GitHub API from your device; there is no Vysio server in the middle handling your token.

## More Room for the Editor
Removing the URL bar, browser tabs, and navigation controls gives the editor more of the screen. With Stage Manager or an external display, the setup starts to feel much closer to a focused desktop workspace.

---

## Getting Started

Vysio is currently in private TestFlight beta. If you want to try the iPad setup without fighting Safari shortcuts, join the waitlist on the homepage and I will send an invite when the next batch opens.
