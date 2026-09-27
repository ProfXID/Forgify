<div align="center">

# ⚡ Forgify

### Local-First LAN Git Client for Game Dev Studios

[![Version](https://img.shields.io/badge/v1.0.9-stable-4F8BFF?style=for-the-badge)](../../releases)
[![Windows](https://img.shields.io/badge/Windows_10%2F11-x64-0078D6?style=for-the-badge&logo=windows&logoColor=white)](../../releases)
[![.NET](https://img.shields.io/badge/.NET_10-C%23_13-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](#tech-specs)
[![Zero Deps](https://img.shields.io/badge/NuGet_deps-0-10B981?style=for-the-badge)](#tech-specs)

**Deploy, host, and sync Git repositories across your LAN.**
<br/>No cloud. No subscriptions. No third-party servers. Your code never leaves your network.

<br/>

<img src="docs/assets/forgify-screenshot.png" alt="Forgify — Workspace View" width="720" />

<br/>

[**Download**](../../releases) · [**Changelog**](CHANGELOG.md) · [**EULA**](EULA.md)

</div>

<br/>

---

## The Problem

You're a game studio. Your repos have 10 GB of textures, 3D models, and audio. GitHub charges for LFS bandwidth. GitLab needs a server. You're sitting on a gigabit LAN doing nothing.

**Forgify turns any Windows PC into a Git host.** One click — teammates clone, push, and pull at full LAN speed.

<br/>

<table>
<tr>
<td width="50%">

### What you get

- 🖥️ Full Git hosting on any workstation
- ⚡ LAN-speed push/pull (no internet needed)
- 📦 Git LFS with bandwidth control
- 👥 Real-time peer discovery & presence
- 💬 Encrypted P2P chat between peers
- 🛡️ Per-project access control & invites
- 🌐 6 languages built-in

</td>
<td width="50%">

### What you skip

- ~~Monthly cloud hosting bills~~
- ~~Storage & bandwidth quotas~~
- ~~Internet dependency~~
- ~~SSH key ceremonies~~
- ~~Docker/Linux server setup~~
- ~~Third-party account signups~~
- ~~Uploading proprietary assets to the cloud~~

</td>
</tr>
</table>

<br/>

---

## Core Features

<table>
<tr>
<td width="60">⚡</td>
<td>
<strong>Embedded Git Host Server</strong><br/>
<sub>Start a server on any PC with one click. Full Git Smart HTTP protocol — <code>git-upload-pack</code>, <code>git-receive-pack</code>, and LFS with chunked transfer. Repos are vaulted at <code>&lt;Drive&gt;:\git-forgify\host\</code> — isolated per user and project.</sub>
</td>
</tr>
<tr>
<td width="60">👥</td>
<td>
<strong>LAN Peer Discovery</strong><br/>
<sub>UDP broadcast auto-discovers teammates on your network. See who's online, what project they're in, and their sync status — updated every 3 seconds. Zero configuration.</sub>
</td>
</tr>
<tr>
<td width="60">🔐</td>
<td>
<strong>Security & Access Control</strong><br/>
<sub>HMAC-SHA256 signed session tokens, IP-bound with 7-day expiry. ECDSA presence proofs on every mutation. Per-project member ACLs with time-limited invite tickets (30s expiry). Pairing key authentication at the transport layer.</sub>
</td>
</tr>
<tr>
<td width="60">📦</td>
<td>
<strong>SmartSync</strong><br/>
<sub>Not a blind <code>git pull</code>. Analyzes ahead/behind state, predicts conflicts before they happen, stages selected files, and creates safety stash checkpoints automatically.</sub>
</td>
</tr>
<tr>
<td width="60">💬</td>
<td>
<strong>Encrypted P2P Chat</strong><br/>
<sub>Direct messaging between LAN peers. AES-256 encrypted at rest. Messages queue offline and auto-deliver when peers reconnect. No chat server needed.</sub>
</td>
</tr>
<tr>
<td width="60">🛡️</td>
<td>
<strong>Smart Protection</strong><br/>
<sub>One-click <code>.gitignore</code> and <code>.gitattributes</code> templates for Unity, Unreal, and general game dev — with Git LFS tracking rules pre-configured.</sub>
</td>
</tr>
</table>

<br/>

---

## Quick Start

```
1.  Download & install           →  ForgifySetup-v1.0.9.exe
2.  Set up your identity         →  Display name + email
3.  Choose your host vault       →  Select drive for git-forgify/
4.  Create a project             →  New Project → pick local path
5.  Start hosting                →  Toggle Host Server ON
6.  Invite teammates             →  Share token or send direct invite
```

> The installer auto-detects Git, configures firewall rules (TCP 5050, UDP 5051), and supports 6 languages.

<br/>

---

## Architecture

```
                          ┌───────────────────────────────────┐
                          │          Forgify  (WPF)           │
                          ├───────────┬───────────┬───────────┤
                          │ Projects  │ Workspace │ LAN Peers │
                          │ Manager   │  Git Ops  │ & Chat    │
                          ├───────────┴───────────┴───────────┤
                          │       R2G.Forgify.Runtime         │
                          │                                   │
                          │  Git Engine    HTTP :5050          │
                          │  (CLI)         UDP  :5051          │
                          │  Chat Repo     Hub Manifest        │
                          ├───────────────────────────────────┤
                          │ .NET 10 · C# 13 · Win32 · 0 deps │
                          └──────────┬──────────┬─────────────┘
                                     │          │
                               ┌─────┴──┐  ┌───┴──────────┐
                               │ Your   │  │ git-forgify/  │
                               │ repos  │  │  host/        │
                               │        │  │  chats/       │
                               └────────┘  │  hub.json     │
                                           └───────────────┘
```

<br/>

---

## Tech Specs

| | |
|:--|:--|
| **Runtime** | .NET 10 — self-contained, no framework install needed |
| **Language** | C# 13 |
| **UI** | WPF (Windows Presentation Foundation) |
| **NuGet Dependencies** | **0** — stdlib + native Win32 only |
| **Git** | CLI-based process execution |
| **LFS** | Custom HTTP handler with chunked transfer & bandwidth limiter |
| **Crypto** | AES-256 (chat) · HMAC-SHA256 (sessions) · ECDSA (presence) |
| **Signing** | Authenticode SHA-256, RSA 3072-bit |
| **Installer** | Inno Setup 6.7.3 with EULA scroll-to-unlock |
| **Tests** | 44 automated checks (GitEngineCheck) |
| **Languages** | English · Indonesian · Spanish · Japanese · Russian · Chinese |
| **Display** | Min 1200×780, High-DPI aware |

<br/>

---

## Network

| Port | Protocol | Role |
|:-----|:---------|:-----|
| `5050` | TCP / HTTP | Git transport, Hub API, Chat API, Permissions |
| `5051` | UDP | Peer discovery beacon (broadcast) |

> Both ports are auto-registered in Windows Firewall during admin-mode installation.

<br/>

---

## Data Ownership

> **Your code is yours. Period.**

Forgify is engineered as an offline-first, local-network tool.

- **Zero cloud uploads** — no files, telemetry, or credentials leave your machines
- **Zero third-party sync** — all data travels over your physical LAN
- **Zero accounts required** — no GitHub, GitLab, or Bitbucket signup needed
- **One optional outbound connection** — update checks via GitHub Releases (can be disabled)

All source code, assets, repositories, commit histories, and chat messages remain the exclusive property of the user. Run2Go Studio claims zero ownership over your work.

<br/>

---

## Verification

Every release binary is Authenticode-signed by Run2Go Studio.

```
Signer      Run2Go Studio
Thumbprint  94AE8C466AB7787260AD72DF9202C73F237CC8B1
Algorithm   SHA-256 RSA 3072-bit
```

```powershell
# Verify any Forgify binary
signtool verify /pa /v Forgify.exe
```

<br/>

---

## Project Structure

```
Forgify/
├── src/                              # Application source
│   ├── MainWindow.xaml               # Primary WPF interface
│   ├── R2G.Forgify.Runtime/          # Core engine (Git, HTTP, UDP, crypto)
│   └── Localization/                 # 6 language resource dictionaries
├── tests/GitEngineCheck/             # 44-test automated verification
├── tools/
│   ├── installer.iss                 # Inno Setup installer script
│   ├── build_standalone.py           # Build, obfuscate & sign pipeline
│   └── certs/                        # Authenticode certificates
├── build-standalone/                 # Self-contained win-x64 binary
├── installer/                        # Signed installer (.exe)
├── CHANGELOG.md
├── EULA.md
└── README.md
```

<br/>

---

## License

Forgify is proprietary software by [**Run2Go Studio**](https://github.com/Run2Go).

| | |
|:--|:--|
| ✅ | Personal, indie, educational, and commercial studio use |
| ✅ | Multi-device LAN deployment across workstations |
| ❌ | Redistribution, repackaging, or hosted SaaS |
| ❌ | Reverse engineering of the runtime engine |

Full terms → [EULA.md](EULA.md)

<br/>

---

<div align="center">

<br/>

**Built for studios that keep their code where it belongs.**

<sub>Made with 🤍 by Run2Go Studio · © 2026 · All Rights Reserved</sub>

<br/>

<img src="https://img.shields.io/badge/C%23_13-239120?style=flat-square&logo=csharp&logoColor=white" />
<img src="https://img.shields.io/badge/.NET_10-512BD4?style=flat-square&logo=dotnet&logoColor=white" />
<img src="https://img.shields.io/badge/WPF-0078D6?style=flat-square&logo=windows&logoColor=white" />
<img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white" />
<img src="https://img.shields.io/badge/Inno_Setup_6-4B0082?style=flat-square" />

</div>
