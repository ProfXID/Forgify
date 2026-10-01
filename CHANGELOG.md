# Changelog

All notable changes to Forgify are documented in this file.

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
