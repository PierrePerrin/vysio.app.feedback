---
title: "The complete guide to GitHub Codespaces on iPad in 2026"
date: "2026-06-07"
description: "Step-by-step: set up GitHub Codespaces, connect from your iPad, and work around the browser limitations that make iPadOS coding awkward."
image: "/vysio-ipad-editor.png"
author: "Pierre Perrin"
readTime: "7 min read"
---

GitHub Codespaces is one of the better ways to code from an iPad because the iPad does not have to run the project locally. It only has to render the editor, send your keystrokes, and keep a stable connection to the machine doing the work.

That sounds simple. The rough part is the last mile: Safari, keyboard shortcuts, screen sleep, and session handling. This guide walks through a practical setup for Codespaces on iPad and where a native client like Vysio helps.

## What Is GitHub Codespaces?

GitHub Codespaces is a cloud development environment hosted by GitHub. When you open a Codespace, you get a container running in Microsoft Azure with:

- A full VS Code editor in the browser
- A Linux terminal with root access
- Persistent storage between sessions
- A pre-configured development environment based on your repository's `devcontainer.json`

For iPad users, the critical advantage is that your iPad only needs to render the editor and send keystrokes. All compilation, package installation, and runtime execution happens in the cloud.

Your iPad becomes the screen and keyboard. The Codespace does the heavy lifting.

## Prerequisites

- A GitHub account (free tier includes 60 core-hours per month)
- An iPad running iPadOS 17 or later
- An external keyboard (strongly recommended — the on-screen keyboard will frustrate you)
- Vysio installed from TestFlight if you want the native iPad workflow described below

## Step 1: Create Your First Codespace

Navigate to any repository on GitHub and click the green **Code** button. Select the **Codespaces** tab, then click **Create codespace on main** (or whichever branch you want to work from).

GitHub will provision your container. This typically takes 30 to 90 seconds on first launch. Subsequent starts are much faster because the container's state is preserved.

When provisioning is complete, the browser opens your Codespace in a full VS Code interface. You can start working immediately.

### Choosing a Machine Type

By default, GitHub provides a 2-core machine. For most web development, this is sufficient. If you are working with large codebases, running multiple services, or doing anything compute-intensive, you can upgrade when creating the Codespace by clicking **Configure and create codespace** before confirming.

Machine types range from 2 to 32 cores. Larger machines cost more core-hours, so choose based on your actual needs.

## Step 2: Configure Your Development Container

A `devcontainer.json` file at the root of your repository tells Codespaces what tools to install automatically. Without one, you get a blank Ubuntu container and have to install everything manually each time.

Here is a minimal example for a Node.js project:

```json
{
  "name": "Node.js",
  "image": "mcr.microsoft.com/devcontainers/javascript-node:20",
  "postCreateCommand": "npm install",
  "customizations": {
    "vscode": {
      "extensions": [
        "esbenp.prettier-vscode",
        "dbaeumer.vscode-eslint"
      ]
    }
  }
}
```

Commit this file, then the next Codespace you create from this repository can start with Node 20, your npm dependencies installed, and your preferred extensions ready.

The [Dev Container specification](https://containers.dev) has pre-built images for most languages and frameworks. You rarely need to write a custom Dockerfile.

## Step 3: Connect from iPad — The Browser Route (and Its Limits)

Open Safari on your iPad and navigate to `github.com`. Sign in, open your repository, and launch your Codespace the same way you would on a Mac.

It works. The VS Code interface loads, you can browse files, and basic editing is functional.

Here is where it starts to get annoying:

**Keyboard shortcut conflicts.** Safari intercepts `Cmd + P` (print), `Cmd + W` (close tab), `Cmd + T` (new tab), and `Cmd + N` (new window) before VS Code can receive them. Those are not obscure commands. They are how you find files, close editors, and open terminals.

**Screen sleep.** iOS aggressively suspends background processes. If your iPad screen goes off during a long build or test run, the WebSocket connection to your Codespace drops. When you wake the screen, you need to wait for reconnection before you can see results.

**Session storage.** Safari stores your GitHub session as browser state. That is fine for browsing, but less pleasant when you are trying to treat Codespaces like a daily development tool and suddenly need to sign in again.

These issues are not Safari bugs. They are normal browser behavior showing up in a workflow that expects desktop-editor semantics.

## Step 4: Connect with Vysio — The Native Route

Vysio is a native iPadOS app built for this use case. It wraps Codespaces in a configured `WKWebView` and adds the native pieces Safari does not provide for this workflow.

**Install Vysio** from TestFlight (link on the Vysio homepage) and sign in with your GitHub account using the OAuth flow. Your token is stored in the Apple Keychain, encrypted and locked behind Face ID.

**Open your Codespace** by selecting it from the native dashboard. Vysio lists all your Codespaces with their current status — running, stopped, or starting — and lets you start and stop them without opening a browser.

Once your Codespace opens in Vysio's editor view:

- `Cmd + P` opens VS Code's file finder
- `Cmd + W` closes the active editor tab
- `Cmd + T` opens a new terminal (if configured in VS Code)
- `Cmd + Shift + P` opens the command palette

Those shortcuts pass directly to VS Code without being intercepted by the browser.

The screen stays on while a workspace is active. A long build can keep running while you read documentation or check an API reference, and you can come back to the same connected terminal.

## Step 5: Optimize Your Workflow

### Use the VS Code Command Palette Heavily

`Cmd + Shift + P` is one of the most useful shortcuts on iPad. Most VS Code actions are accessible through it, and it works cleanly in Vysio. Learn to run tasks, open terminals, switch themes, and install extensions from the keyboard.

### Port Forwarding for Web Development

When your development server starts (say, on port 3000), Codespaces automatically creates a forwarded port. You can open the preview URL — in the format `https://<codespace-name>-3000.app.github.dev` — directly in a browser tab or in a Vysio port preview.

### Persisting Environment Between Sessions

Codespaces saves your open files and terminal history between sessions. When you stop a Codespace and restart it later, you return to approximately where you left off. This is different from rebuilding the container — a rebuild starts fresh but re-runs your `devcontainer.json` setup steps.

Stop your Codespace when you finish working to avoid burning core-hours. GitHub will also automatically stop idle Codespaces after a configurable timeout (default 30 minutes).

### Manage Costs

GitHub's free plan includes a monthly allowance of core-hours and storage. For occasional use, it may be enough; for daily work, it is worth checking your billing settings before you leave a larger Codespace running all afternoon.

Stop your Codespace when you finish working, and set a sensible idle timeout in GitHub. Larger machines are useful, but they consume the allowance faster.

## The Result

With a Codespace configured for your project and Vysio handling the connection from your iPad, the setup stops feeling like a browser workaround and starts feeling like a normal development environment.

Your keyboard works. Your screen stays on. Your credentials are secure. Your code lives in a real Linux container with real tools.

If you want to try it, join the Vysio TestFlight beta from the homepage.
