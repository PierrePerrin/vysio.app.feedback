---
title: "Magic Keyboard + iPad + GitHub Codespaces: the developer's setup guide"
date: "2026-05-31"
description: "How to set up a keyboard-first iPad development workflow with GitHub Codespaces, hardware keyboards, and shortcuts that actually reach your editor."
image: "/vysio-ipad-editor.png"
author: "Pierre Perrin"
readTime: "6 min read"
---

If you code on iPad, you already know the keyboard situation is complicated. iPadOS handles keyboard input differently from macOS, and cloud editors like VS Code add another layer on top. The hard part is not typing code. It is getting the shortcuts you use all day to reach the editor instead of the system or the browser.

This guide covers the keyboards worth using, the shortcuts that matter most, and where the browser gets in the way.

## Choosing a Keyboard

Not all keyboards behave the same way on iPad. The differences matter for developers.

### Apple Magic Keyboard for iPad Pro

Usually the cleanest option if you own an iPad Pro. It connects via the Smart Connector (no Bluetooth pairing, no batteries), snaps magnetically into place, and includes a trackpad that works well with iPadOS's pointer model.

For development, the key advantage is that it has a full set of modifier keys — `Cmd`, `Option`, `Control`, `Shift` — and they behave exactly as you would expect from a Mac keyboard. Function keys are available via `Fn` combinations.

The one omission that frustrates developers is the lack of a dedicated `Escape` key. In Vim mode or any terminal, `Escape` is constant. You can remap `Caps Lock` to `Escape` in iPadOS Settings under **General → Keyboard → Hardware Keyboard → Modifier Keys**.

### Apple Magic Keyboard (Universal)

The standalone Magic Keyboard connects via Bluetooth and works with any iPad. It includes a full key layout and feels familiar if you already use a Mac keyboard. The tradeoff is Bluetooth pairing latency on initial connection and no trackpad.

For desk setups, it is excellent. For mobile use, you lose the integrated kickstand of the folio keyboards.

### Logitech MX Keys Mini for Mac

A compact wireless keyboard that supports three device pairing via the `Easy-Switch` buttons. The Mac-specific version has the correct modifier key labeling for iPadOS. The compact layout removes the numpad without sacrificing the arrow keys, which matters for navigation shortcuts.

It is battery-powered, rechargeable over USB-C, backlit, and comfortable to type on. It is a good choice if you move between iPad and a Mac or PC.

### What to Avoid

Generic Windows USB keyboards can work, but the modifier key positions (`Ctrl`, `Alt`, `Windows`) do not map cleanly to iPadOS conventions. You may find yourself pressing the wrong keys until you remap the modifiers in iPadOS settings.

Avoid Bluetooth keyboards that require a PIN pairing step — most do not, but some older models do, and the iPad re-pairs on every reconnect, which becomes irritating quickly.

## The Keyboard Shortcut Problem in Browsers

Here is the core issue: when you open VS Code in Safari, iPadOS and Safari both want to handle keyboard shortcuts. They get priority. VS Code receives only what they do not claim.

The shortcuts they claim are exactly the ones you use most:

| Shortcut | iPadOS/Safari action | VS Code intended action |
|----------|---------------------|------------------------|
| `Cmd + P` | Print dialog | Open file finder |
| `Cmd + W` | Close browser tab | Close editor tab |
| `Cmd + T` | New browser tab | New terminal |
| `Cmd + N` | New browser window | New file |
| `Cmd + ,` | (varies) | Open settings |

This is not a VS Code bug. Safari is behaving as expected. It simply does not know you want to code.

## Fixing It: Native Keyboard Passthrough with Vysio

Vysio solves this at the WebKit layer. Instead of running VS Code inside Safari, Vysio wraps it in a custom `WKWebView` configured to suppress system-level shortcut interception. Keyboard events pass directly to the web content before iPadOS can act on them.

After installing Vysio and opening your Codespace through it, the common editor shortcuts work as intended:

- `Cmd + P` → VS Code file finder
- `Cmd + W` → closes the active editor tab
- `Cmd + T` → new terminal panel
- `Cmd + N` → new untitled file
- `Cmd + Shift + P` → command palette

No Safari tab closing, no print dialog when you wanted the file picker, and no custom VS Code remapping just to get through a normal session.

## The Shortcuts That Matter Most

Once keyboard passthrough works, focus on learning these. They cover most of a normal coding session.

### Navigation
- `Cmd + P` — Go to file (most important shortcut in VS Code)
- `Cmd + Shift + E` — Toggle file explorer
- `Cmd + B` — Toggle sidebar
- `` Ctrl + ` `` — Toggle integrated terminal
- `Cmd + Shift + F` — Search across all files
- `` ` `` — Switch between editor groups

### Editing
- `Cmd + D` — Select next occurrence of current word
- `Option + Click` — Add a cursor at click position
- `Cmd + Shift + K` — Delete line
- `Option + Up/Down` — Move line up or down
- `Cmd + /` — Toggle line comment
- `Cmd + Z` / `Cmd + Shift + Z` — Undo / Redo

### Running Code
- `Cmd + Shift + P` then type "Run Task" — trigger any configured task runner
- `` Ctrl + Shift + ` `` — New terminal panel
- `Cmd + Shift + B` — Run build task

### VS Code Specific
- `Cmd + K, Cmd + S` — Open keyboard shortcuts editor (useful for remapping)
- `Cmd + Shift + X` — Open extensions panel
- `Cmd + ,` — Open settings

## Trackpad Gestures for Developers

If you use the Magic Keyboard with trackpad, these gestures speed up navigation in VS Code:

- **Two-finger scroll** in the file explorer to navigate quickly
- **Click and drag** to select code — more precise than touch selection
- **Two-finger click (right-click)** for context menus in the editor gutter
- **Three-finger swipe up** to see all open windows (App Exposé)

The pointer model on iPadOS 17+ is good enough for daily development. It does not behave identically to macOS — hover states are slightly different, and some UI elements still feel sized for touch — but it is no longer the weak point of the setup.

## Suggested Workspace Layout

With a Magic Keyboard and the trackpad, consider this layout for focused work:

1. **Vysio in full screen** — no distractions, no dock, no status bar visible
2. **Explorer sidebar closed** — use `Cmd + P` to navigate files instead
3. **Two editor columns** — main file on the left, reference or test file on the right
4. **Terminal panel in the bottom third** — always visible, sized to show 8-10 lines

You can save this layout using VS Code's built-in "Profiles" feature, so it restores every time you open Vysio.

## External Display

iPad Pro supports external displays via USB-C. If you connect a monitor, you get a second screen in Stage Manager. Vysio runs in its own Stage Manager window, so you can keep VS Code on your external display and use the iPad's built-in screen for documentation, terminal, or browser previews.

This is where the iPad Pro setup starts to feel less like a tablet compromise. The external display can run at its native resolution (up to 6K on Apple Studio Display), the trackpad controls both screens, and Vysio keeps your Codespace alive throughout.

## One Last Thing

None of this requires a high-end iPad. The development compute happens in the Codespace, not on your iPad. A 2016 iPad Pro would run Vysio and render VS Code just as well as an M4, assuming it supports iPadOS 17.

The keyboard matters more than the chip. Pick one that feels right, get the shortcuts working, and then tune the workspace around that.

If you want to try the full setup, join the Vysio beta from the homepage.
