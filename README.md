# Forgify

Local-first Git collaboration for Windows teams.

[Download the latest release](../../releases) · [Changelog](CHANGELOG.md) · [License](EULA.md)

![Forgify workspace](docs/assets/forgify-screenshot.png)

Forgify turns a Windows workstation into a Git and Git LFS host for teammates on the same local network. It provides repository hosting, project access controls, discovery, synchronization, and team communication without requiring a separate server.

## Features

- Embedded Git Smart HTTP hosting
- Git LFS support with configurable bandwidth limits
- Automatic host discovery on the local network
- Project access controls and invitation management
- Encrypted LAN messaging
- SmartSync for project updates
- Built-in `.gitignore` and `.gitattributes` templates
- Interface available in six languages
- Optional automatic startup in background mode

## Requirements

- Windows 10 or Windows 11, 64-bit
- Git for Windows with Git LFS
- A local network connection between the host and client workstations

Forgify is distributed as a self-contained .NET 10 application, so users do not need to install the .NET runtime separately.

## Getting started

1. Download `ForgifySetup-v1.0.10.exe` from the [Releases](../../releases) page.
2. Install Forgify and create a developer account.
3. Choose a Host Vault directory for repositories and Git LFS objects.
4. Add an existing project or create a new one.
5. Share the project with teammates discovered on the same network.

## Network configuration

| Protocol | Port | Purpose |
| --- | ---: | --- |
| TCP | `5050` | Git Smart HTTP, Git LFS, API, and WebSocket traffic |
| UDP | `5051` | Local network discovery |

If Windows Firewall prompts for access, allow Forgify on private networks. Repository and LFS transfers remain on the local network. Account sign-in, avatar retrieval, and update checks may require internet access.

## Build from source

Prerequisites:

- .NET 10 SDK
- Python 3
- Inno Setup 6 for installer generation

Build the solution:

```powershell
dotnet build Forgify.sln -c Release
```

Create the standalone package and installer:

```powershell
python tools\build_standalone.py --installer
```

Run the verification projects:

```powershell
dotnet run --project tests\GitEngineCheck\GitEngineCheck.csproj -c Release
dotnet run --project tests\StandaloneCheck\StandaloneCheck.csproj -c Release
```

## Project structure

```text
src/                  WPF application and embedded Git/Git LFS runtime
installer/            Inno Setup configuration and release installer
tests/                 Git engine and standalone verification projects
tools/                 Build and packaging scripts
docs/                  Product documentation and assets
```

## Release integrity

Release binaries are Authenticode-signed by **Run2Go Studio**.

- Certificate thumbprint: `94AE8C466AB7787260AD72DF9202C73F237CC8B1`
- `v1.0.10` installer SHA-256: `12D9C700B22F8C19FE17DD57BC4FB2F18BBBD24475B0824D782711389683CB2A`

Verify a downloaded installer in PowerShell:

```powershell
Get-FileHash .\ForgifySetup-v1.0.10.exe -Algorithm SHA256
Get-AuthenticodeSignature .\ForgifySetup-v1.0.10.exe
```

The current distribution certificate is self-signed. Windows may show an untrusted publisher warning until the Run2Go Studio certificate is installed as a trusted root.

## License

Forgify is proprietary software. Installation and use are governed by the [End User License Agreement](EULA.md).

Copyright © 2026 Run2Go Studio. All rights reserved.
