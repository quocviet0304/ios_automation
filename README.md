# ⚡ QvAuto - High-Performance iOS UI Automation & UI Hierarchy Engine (like uiautomator2 for iOS)

<p align="center">
  <img src="CydiaIcon.png" width="120" height="120" style="border-radius: 26px; box-shadow: 0 8px 24px rgba(0,122,255,0.35);" alt="QvAuto Logo">
</p>

<p align="center">
  <b>The Ultra-Fast, Standalone & Remote iOS Automation Daemon with Full UI Hierarchy Dump (uiautomator2 Alternative for iOS)</b>
</p>

<p align="center">
  <a href="https://t.me/viethappy_0205"><img src="https://img.shields.io/badge/Telegram-@viethappy__0205-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram Contact"></a>
  <img src="https://img.shields.io/badge/iOS-14.0%20--%2016.6.1-007AFF?style=for-the-badge&logo=apple&logoColor=white" alt="iOS Support">
  <img src="https://img.shields.io/badge/Architecture-arm64%20(Rootless%20%26%20Rootful)-success?style=for-the-badge" alt="Architecture">
  <img src="https://img.shields.io/badge/Speed-15ms%20Latency-orange?style=for-the-badge" alt="Speed">
</p>

---

## 🌟 Overview

**QvAuto** is an enterprise-grade iOS automation framework engineered specifically for Jailbroken iOS devices (iOS 14.0 – 16.6.1). 

Acting as the **iOS counterpart to Android's `uiautomator2`**, QvAuto provides instant **UI hierarchy tree dumping (XML/JSON)**, element inspection, low-level kernel touch injection (`IOHIDEvent`), on-device Neural Engine OCR, and an embedded **REST API on port `8080`** — completely eliminating the need for bulky frameworks like Appium or WebDriverAgent.

```
                   ┌────────────────────────────────────────────────────────┐
                   │                  WINDOWS / MAC / LINUX                 │
                   │        Python / Node.js / Go / C# / Java / cURL        │
                   └───────────────────────────┬────────────────────────────┘
                                               │ USB (iproxy) / Wi-Fi (LAN)
                                               ▼
┌──────────────────────────────────────────────────────────────────────────────────────────┐
│                                   IPHONE (JAILBROKEN)                                    │
│                                                                                          │
│  ┌────────────────────────────────────────────────────────────────────────────────────┐  │
│  │                     QvAuto Embedded HTTP Server (Port 8080)                        │  │
│  └─────────────────────────────────────┬──────────────────────────────────────────────┘  │
│                                        ▼                                                 │
│  ┌────────────────────────────────────────────────────────────────────────────────────┐  │
│  │                               CORE AUTOMATION ENGINE                               │  │
│  │                                                                                    │  │
│  │  🌳 UI Hierarchy Dump : Native AXRuntime XML / JSON tree (like uiautomator2)        │  │
│  │  🎯 Element Locators  : By Text, Accessibility ID, Class, Bounds, XPath             │  │
│  │  ⚡ Touch Injection   : Low-Level IOHIDEvent (Tap, Swipe, Drag, Multi-Touch)       │  │
│  │  👁 Neural Engine OCR : Apple Vision Framework (15-25ms response time)             │  │
│  │  📸 60 FPS Capture    : Zero-lag Direct Framebuffer / IOSurface                     │  │
│  └────────────────────────────────────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🚀 Key Features

### 🌳 1. Native UI Hierarchy Dump (uiautomator2 for iOS)
* **Instant XML / JSON Tree Dump:** Dumps the entire visible and off-screen UI element hierarchy in milliseconds.
* **Rich Node Attributes:** Each element includes:
  - `text` / `label` / `value` / `placeholder`
  - `resource-id` / `accessibilityIdentifier`
  - `type` / `class` (e.g. `Button`, `StaticText`, `TextField`, `Table`, `Cell`)
  - `bounds` / `frame` (`[x, y, width, height]`)
  - `enabled`, `clickable`, `focused`, `selected`, `visible`
* **Element Selectors & XPath:** Find and interact with elements by XPath, text matching (exact/contains/regex), or Accessibility ID without manual coordinate guessing.

### ⚡ 2. Kernel-Level Touch & Key Simulation (`IOHIDEvent`)
* Dispatches genuine hardware-level touch events via `backboardd`.
* Natural gesture synthesis: Taps, Swipes, Drags, Long-Press, Multi-touch Pinches, and Hardware Button clicks (Home, Lock, Volume).
* Fast text typing and IME input injection without clipboard delays.

### 👁 3. Neural Engine Vision AI & Screen Capture
* **Hardware-Accelerated OCR:** Powered by Apple's `Vision.framework` and Apple Neural Engine (NPU), parsing complete screen text in **15–25ms**.
* **Direct IOSurface Capture:** Ultra high-speed screen streaming and screenshotting at 60 FPS with minimal CPU/battery overhead.

### 🌐 4. 0-Dependency Remote REST API (Port 8080)
* Control hundreds of iPhones concurrently from a single PC over standard HTTP requests.
* Compatible with Python, Node.js, C#, Go, Java, or simple `curl` commands.

---

## 📲 Quick Installation via Sileo / Zebra / Cydia

### Method 1: Add APT Repository (Recommended)
1. Open **Sileo** (or **Zebra / Cydia**) on your jailbroken iPhone.
2. Navigate to **Sources** $\rightarrow$ Tap the **"+"** button.
3. Enter the repository URL:
   ```
   https://quocviet0304.github.io/ios_automation/
   ```
4. Tap **Add Source**.
5. Search for **`QvAuto`** and tap **Get / Install**.

---

## 💻 Python Quickstart (uiautomator2 Style)

You can easily automate iOS just like you do with `uiautomator2` on Android:

```python
import requests

IPHONE_URL = "http://192.168.1.100:8080"

# 1. Dump UI Hierarchy (XML / JSON Tree)
tree = requests.get(f"{IPHONE_URL}/api/v1/accessibility/hierarchy").json()
print("UI Hierarchy:", tree)

# 2. Find Element by Text or Accessibility ID & Tap
requests.post(f"{IPHONE_URL}/api/v1/accessibility/tap", json={
    "text": "Log In",
    "exact": True
})

# 3. Simulate Fast Hardware Touch (Tap at X, Y)
requests.post(f"{IPHONE_URL}/api/v1/touch/tap", json={"x": 200, "y": 450})

# 4. Instant On-Device Neural Engine OCR
ocr_results = requests.post(f"{IPHONE_URL}/api/v1/vision/ocr", json={}).json()
for item in ocr_results.get("results", []):
    print(f"Found text: '{item['text']}' at ({item['center_x']}, {item['center_y']})")
```

---

## 🛠 Compatibility & Supported Environments

| Parameter | Specification |
| :--- | :--- |
| **iOS Versions** | iOS 14.0 – 16.6.1 (arm64 / arm64e) |
| **Jailbreak Environments** | Dopamine (Rootless), Dopamine (Rootful), Palera1n, XinaA15, Taurine, unc0ver |
| **Connectivity** | USB Lightning/Type-C (via `iproxy` port forward) or Wi-Fi Local Area Network (LAN) |
| **Payload Size** | Lightweight native binary (< 2.5 MB) |

---

## 💬 Commercial License & Support

For enterprise automation setups, custom feature integration, and commercial License Keys:

* **Telegram:** [@viethappy_0205](https://t.me/viethappy_0205) *(Available 24/7)*
* **Direct Chat Link:** [https://t.me/viethappy_0205](https://t.me/viethappy_0205)

---

<p align="center">
  <b>© 2026 QvAuto Team. High-Performance iOS Automation Engine.</b>
</p>
