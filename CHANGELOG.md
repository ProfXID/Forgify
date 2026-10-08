# Changelog

All notable changes to Forgify are documented in this file.

## [1.0.12] - 2026-10-08

### Fixed

- Fixed false Everything Up to Date on clients left running while the host receives new commits. Host verification expires after 30 seconds and is scoped to the project path, branch, and remote URL.
- SmartSync fetches and verifies the host before selecting Pull, Push, or Up to Date, then releases the interaction lock before the next action.
- Failed host checks remain Offline/FAILED after local refresh. Focus/restore checks stale state, and peer completion invalidates cached host evidence.
- Fetch uses progress, cancellation, and a 120-second inactivity timeout. An active transfer can exceed six seconds; another origin cannot hide a host failure.

### Changed

- Aligned application, runtime, launcher, UI, updater, and installer metadata to `1.0.12` so existing `1.0.11` installations can upgrade.
- Installer builds use `installer/v.<version>/`; previous release artifacts are preserved.

### Release verification

- GitEngineCheck: **44/44 passed against the source build**. The full suite uses private-method reflection that is incompatible with runtime obfuscation.
- Published runtime passed `--sync-safety` and `--remote-sync`, including stale state, restart, branch/URL isolation, failed fetch/local refresh, origin isolation, incoming commits, active fetch longer than six seconds, and cancellation.
- Published application/runtime passed WPF remote-sync, welcome/Hub, tray restore, simulated shutdown/logoff, and manual-exit checks.
- Self-contained .NET 10 `win-x64` publish, runtime obfuscation, StandaloneCheck with Git/LFS transfer and invitation/clone flows, and Inno Setup compilation passed.
- Launcher, application executable, runtime, and installer have valid Run2Go Studio Authenticode signatures matching the updater signer pin.
- ZIP contents match all 251 standalone files, including six localization XML files. Final signed artifact checksums match the release manifest.
- One existing `SYSLIB0057` warning remains. Actual two-PC operation and installer execution were not tested; artifacts have not been uploaded.

### Artifacts

- Installer: `installer/v.1.0.12/ForgifySetup-v1.0.12.exe` (45,968,776 bytes)
- Installer SHA-256: `CBF61F27D065DE464FF1DD1050E3FCDFC6E297232E2DF170C5D72373F0E5CEA8`
- Standalone ZIP: `installer/v.1.0.12/Forgify-v1.0.12-win-x64.zip` (61,378,482 bytes)
- ZIP SHA-256: `F6B608888878678CC999EEE02ACF0D60072A88AF119F70A6B2589010F7498035`
- Checksums: `installer/v.1.0.12/SHA256SUMS-v1.0.12.txt`
- Local update manifest targets GitHub tag `v1.0.12`; remote publication remains separate.

## [1.0.11] - 2026-10-02

### Fixed

- Fixed a dark or black startup view by starting initialization after the first WPF content render and keeping the Projects Hub visible beneath the welcome animation.
- Silenced notifications during Windows shutdown, restart, logoff, and manual exit. Audio players are stopped and released, tray notifications are removed, and queued notifications or window restores are suppressed.
- Removed the gray background behind the branch list during project loading. Branch selection, creation, and deletion remain disabled until the Git operation finishes.

### Changed

- **Start with Windows** now opens the normal application window with the welcome animation for configured accounts.
- Legacy `/background` and `--background` arguments now follow the same visible startup flow. Incomplete account or Host Vault setup still opens onboarding.
- Updated startup descriptions in all six interface languages.
- Aligned the application, runtime, launcher, updater, and installer version to `1.0.11`.

### Release verification

- GitEngineCheck: **44/44 tests passed**.
- Self-contained .NET 10 `win-x64` publish, runtime obfuscation, and StandaloneCheck completed successfully.
- WPF checks passed against the published application and runtime: welcome/Hub rendering, tray restore, simulated shutdown/logoff, quiet manual exit, and branch controls disabled during loading and restored afterward.
- Inno Setup 6.7.3 compilation completed successfully.
- The launcher, application executable, runtime, and installer have valid Run2Go Studio Authenticode signatures.
- The standalone ZIP contains all 251 package files; checked binary and localization payloads match the standalone folder.
- One existing `SYSLIB0057` warning remains in updater certificate loading. Actual Windows login/shutdown and installer execution were not tested in this release check.

### Artifacts

- Installer: `installer/ForgifySetup-v1.0.11.exe`
- Installer size: `45,966,360 bytes`
- Installer SHA-256: `33F0F2AE35B7FF7D23780FF3FE7D7BA8A53229CB6625178474EEFEFF58832F8C`
- Standalone ZIP: `installer/Forgify-v1.0.11-win-x64.zip`
- ZIP size: `63,603,260 bytes`
- ZIP SHA-256: `EF3D2F82BFF41D1878D96A5B3858C3B28FDC37A15EFC42A5F5901B197F04F002`
- Checksum file: `installer/SHA256SUMS-v1.0.11.txt`
- The update manifest targets GitHub release tag `v1.0.11` and contains the signed installer SHA-256.

## [1.0.10] - 2026-10-01

### Fixed

- Prevented the WPF window from appearing as a black frame when Forgify starts with Windows in `/background` mode.
- Preserved the welcome animation and normal window behavior for interactive launches.
- Kept onboarding and configuration errors visible when the developer account or Host Vault is not configured correctly.

### Changed

- Startup now selects interactive or background initialization before the main window is displayed.
- Background mode initializes the system tray, LAN discovery, and Git host without showing the main window.
- Updated the application, runtime, standalone package, and installer version to `1.0.10`.

### Release verification

- Release build completed successfully.
- GitEngineCheck: **44/44 tests passed**.
- Self-contained .NET 10 `win-x64` publish completed successfully.
- Runtime obfuscation and StandaloneCheck completed successfully.
- Inno Setup 6.7.3 compilation completed successfully.
- The standalone application, runtime, and installer were signed by Run2Go Studio.

### Artifacts

- Installer: `installer/ForgifySetup-v1.0.10.exe`
- Size: `45,970,656 bytes`
- SHA-256: `12D9C700B22F8C19FE17DD57BC4FB2F18BBBD24475B0824D782711389683CB2A`

## [1.0.9] - 2026-09-27

### Added

- Added a **Start with Windows** option to the Developer Account dialog.
- Enabled automatic startup by default, with a persistent user setting to disable it.
- Added background startup through the `/background` argument when the developer account and Host Vault configuration are valid.
- Added installed-version detection across per-user, per-machine, 32-bit, and 64-bit Windows uninstall registry entries.
- Added localized "Forgify is already installed" messages in English, Indonesian, Spanish, Japanese, Russian, and Simplified Chinese.

### Changed

- The installer now exits before opening the setup wizard when the same version is already installed.
- Upgrades and downgrades to a different version remain supported without requiring EULA acceptance again.
- New installations still require the user to read and accept the EULA.
- Automatic startup configuration is now managed entirely by the application instead of the installer.
- Aligned the Forgify application, R2G.Forgify.Runtime, UI, UpdateService, standalone package, and installer version to `1.0.9`.

### Security and data safety

- Restricted automatic updates to HTTPS URLs with a valid SHA-256 digest and a valid Authenticode signature from the pinned Run2Go Studio certificate.
- Updates are downloaded to a unique partial file, verified before execution, and removed when validation fails.
- **Remove Project** now moves Git metadata to `.forgify-recovery` instead of deleting it permanently. The recovery flow includes path-containment, reparse-point, collision, rollback, and persistence checks.
- Preserved `.gitignore`, `.gitattributes`, and `.gitmodules` when removing a project from Forgify.
- **Discard All** now fails closed: a safety stash must be created and verified before local changes are discarded.
- Removed the destructive `checkout -- .` fallback and automatic deletion of untracked files.

### Fixed

- Fixed a duplicate variable name in TEST 43 that prevented GitEngineCheck from compiling.
- Background startup no longer hides onboarding or error messages when the developer account or Host Vault is not configured correctly.
- The uninstaller now removes the Forgify automatic startup registry entry.

### Release verification

- Self-contained .NET 10 `win-x64` publish completed successfully.
- R2G.Forgify.Runtime obfuscation completed successfully.
- StandaloneCheck completed successfully.
- GitEngineCheck: **44/44 tests passed**.
- Inno Setup 6.7.3 compilation completed successfully.
- The standalone application, runtime, and installer were signed by Run2Go Studio.

### Artifacts

- Installer: `installer/ForgifySetup-v1.0.9.exe`
- Size: `45,967,928 bytes`
- SHA-256: `C7A8F225AFBC16B72E1D7E038557CE0CB6C52C9D5006A18BE48553F933E8FC67`

### Upgrade notes

- Users on `1.0.8` can run the `1.0.9` installer directly; the EULA page is skipped during the upgrade.
- Running the `1.0.9` installer when `1.0.9` is already installed displays a message and closes the installer.
- The Run2Go Studio distribution certificate is self-signed. Windows may report an untrusted root until the studio certificate is installed as a trusted root.

## [1.0.8] - 2026-09-27

- Baseline release before update hardening, recoverable project removal, application-managed automatic startup, and version-aware installer behavior.
