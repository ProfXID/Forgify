a/D:\APPS PROJECTS\Forgify\README.md → b/D:\APPS PROJECTS\Forgify\README.md
@@ -0,0 +1,281 @@
+<p align="center">
+  <img src="docs/assets/forgify-banner.png" alt="Forgify Banner" width="100%" />
+</p>
+
+<h1 align="center">Forgify</h1>
+
+<p align="center">
+  <strong>Local-First LAN Git Client for Game Development Studios</strong>
+</p>
+
+<p align="center">
+  <img src="https://img.shields.io/badge/version-1.0.9-blue?style=flat-square" alt="Version" />
+  <img src="https://img.shields.io/badge/platform-Windows%2010%2F11-0078D6?style=flat-square&logo=windows" alt="Platform" />
+  <img src="https://img.shields.io/badge/.NET-10.0-512BD4?style=flat-square&logo=dotnet" alt=".NET" />
+  <img src="https://img.shields.io/badge/dependencies-0%20NuGet-10B981?style=flat-square" alt="Zero Dependencies" />
+  <img src="https://img.shields.io/badge/license-proprietary-lightgrey?style=flat-square" alt="License" />
+</p>
+
+<p align="center">
+  Deploy, host, and manage Git repositories across your local network — <br/>
+  no cloud, no subscriptions, no third-party servers. Your code stays on your machines.
+</p>
+
+---
+
+## Why Forgify?
+
+Most Git clients assume you have internet. Most Git hosting assumes you want the cloud.
+
+**Forgify assumes neither.**
+
+Built for game development studios, indie teams, and creative professionals who work with large binary assets (textures, 3D models, audio, builds) on a local network — Forgify gives you the collaboration power of GitHub without sending a single byte outside your LAN.
+
+| What You Get | What You Skip |
+|:---|:---|
+| Full Git hosting on any PC | Monthly cloud bills |
+| LAN peer-to-peer sync | Upload/download wait times |
+| Git LFS for large assets | Storage quotas |
+| Real-time team presence | Internet dependency |
+| Built-in encrypted chat | Third-party accounts |
+
+---
+
+## Features
+
+### 🔧 Embedded Git Host Server
+Every Forgify instance can become a Git host. Start a server on any workstation with one click — teammates clone, push, and pull over HTTP on your local network.
+
+- **Zero setup**: No Linux server, no Docker, no SSH keys
+- **Smart HTTP transport**: Full Git Smart HTTP protocol (`git-upload-pack`, `git-receive-pack`)
+- **Git LFS support**: Large file storage with chunked transfer and bandwidth limiting
+- **Repository vault**: Isolated bare repos at `<Drive>:\git-forgify\host\<user>\<project>.git`
+
+### 👥 LAN Peer Discovery & Presence
+Automatic peer discovery via UDP broadcast — see who's online, what they're working on, and their sync status in real time.
+
+- **UDP 5051 beacon**: `PING`, `PONG`, `ANNOUNCE`, `GOODBYE` with 3-second heartbeat
+- **Live status**: Online / Syncing / Offline indicators per peer
+- **Activity state**: See which project each teammate is actively working on
+- **Zero configuration**: Peers appear automatically on the same network segment
+
+### 🔐 Security & Access Control
+Project-level access control with pairing keys, invite tickets, and per-project member management — all enforced at the transport layer.
+
+- **Pairing key authentication**: Token-based access to hosted repositories
+- **Invite system**: Time-limited (30s) invite tickets with email verification
+- **Session tokens**: HMAC-SHA256 signed, IP-bound, 7-day expiry
+- **Per-project ACL**: Allowlisted contributors with kick/rotate capability
+- **LAN presence proof**: ECDSA-signed identity verification on every mutation
+
+### 💬 Encrypted P2P Chat
+Direct messaging between LAN peers with AES-256 encrypted history — no chat server, no cloud relay.
+
+- **Offline-first**: Messages stored locally at `<Drive>:\git-forgify\chats\`
+- **Auto-sync**: Queued messages delivered when peers reconnect
+- **Encrypted at rest**: `FORGIFY_ENC_V1` magic header with AES-256
+
+### 🛡️ Smart Protection
… omitted 203 diff line(s) across 1 additional file(s)/section(s)
