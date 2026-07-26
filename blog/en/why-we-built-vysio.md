---
title: "Why we built Vysio: the iPad developer experience deserved better"
date: "2026-06-14"
description: "The story behind Vysio: why coding from iPad kept almost working, where the browser got in the way, and why we decided to build a native client."
image: "/vysio-ipad-editor.png"
author: "Pierre Perrin"
readTime: "5 min read"
---

There is a specific kind of frustration that only developers know: when the right tool almost exists.

For the past two years, I have been trying to make iPad my primary development device. Not because it is fashionable. Because an iPad Pro with an M4 chip, a cellular connection, and a Magic Keyboard is genuinely the best portable computer I have ever owned. It is light, silent, has an excellent screen, and lasts all day on battery.

The hardware was ready. The software was not.

## The Setup That Should Have Worked

GitHub Codespaces should have solved it. The power of your development environment was no longer tied to the device in your hands. A VS Code instance in the cloud, full terminal access, persistent storage — all of it accessible from any browser, on any device.

"Any device" — including iPad.

So I tried it. I opened `github.dev` in Safari. It loaded. It looked right. And then I started actually writing code.

Within five minutes, I had:
- Triggered a Safari print dialog trying to open a file with `Cmd + P`
- Accidentally closed my browser tab trying to close an editor tab with `Cmd + W`
- Lost my Codespace connection when the iPad screen dimmed during a long build

The third issue was the most demoralizing. The build was almost done. I looked away for thirty seconds. When I came back, the WebSocket was dead and I had to trigger the build again.

## What We Tried First

The obvious first step was to look for an existing app. Something purpose-built for coding in Codespaces from iPad.

There was nothing. Not quite.

There were SSH clients, which solve a different problem. There were general-purpose editors. There were experiments and shortcuts shared on Reddit. I could not find something that treated the iPad as a serious client for the tools I already used: Codespaces, VS Code, hardware keyboard shortcuts, and secure GitHub authentication.

So we built it.

## The Decisions That Shaped Vysio

**No backend. Ever.**

The first design decision was the most important: Vysio would never touch your GitHub tokens on a server we control. Your OAuth token lives in the Apple Keychain on your device, locked behind Face ID. Connections to GitHub's API are made directly from your iPad. We have no servers that could be compromised, no databases that could leak your credentials.

This was not a feature. It was a constraint we imposed on ourselves before writing a single line of code.

**WKWebView configured for developers, not for consumers.**

The second decision was technical. We did not want a thin wrapper that just opens a URL. We configured a `WKWebView` layer so editor shortcuts reach the web content instead of being swallowed by Safari-style commands. `Cmd + W`, `Cmd + P`, `Cmd + T`, `Cmd + N` — they pass through to your editor.

**Screen awake, connection alive.**

We implemented a screen wake lock so Vysio keeps your iPad display on while a workspace is open. Long compilations and long test runs no longer depend on you tapping the screen every few minutes.

**Native dashboard, not a browser tab.**

The Codespaces management experience — listing your workspaces, seeing their state, starting and stopping them — happens in a native SwiftUI interface. You see your Codespaces when you open the app, with their current status, before opening an editor.

## What Vysio Is Not

We are frequently asked: "Can Vysio run a local code-server?" or "Does it have a built-in terminal?" The answer is no, and intentionally so.

Vysio is a native client for remote development environments. The compute lives in the cloud. Vysio is the window through which you access it, and it makes that window as clean and reliable as possible on iPad.

We are not trying to replicate a Mac. We are trying to make the iPad work properly with the tools developers already use.

## Where We Are Now

Vysio is in private beta. The most useful feedback so far has been simple: once the browser stops stealing shortcuts and dropping the connection, coding on iPad starts to feel normal.

We are preparing for a public TestFlight release followed by an App Store submission. If you want to be among the first to try it, join the waitlist on our homepage.

The iPad developer experience deserved better. That is what Vysio is for.
