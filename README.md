# ReleaseLens AI support

Record reviewed Android emulator and web scenarios with local narration, captions and evidence. Install the public pre-release from [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=gyanupadhyay.releaselens-ai), or download an audited VSIX from [Releases](https://github.com/gyanupadhyay/releaselens-support/releases). Select **Switch to Pre-Release Version** in VS Code.

[0.2.1 is available as an audited VSIX](https://github.com/gyanupadhyay/releaselens-support/releases/tag/v0.2.1). All release checks passed. The Marketplace update has been submitted and is awaiting validation; its previously published version remains available meanwhile.

## Start here

- [Complete user guide](docs/USER_GUIDE.md): installation, configuration, flow examples, Flutter web semantics, tokens, authentication, outputs, subtitles, cleanup and recovery.
- [CLI and deployment integration](docs/CI_SETUP.md): running the bundled CLI, receipt creation and authenticated APK artifact provenance.
- [Architecture and security boundaries](docs/ARCHITECTURE.md), [review fixes](docs/REVIEW_FIXES.md), [changelog](CHANGELOG.md).
- [Troubleshooting](docs/TROUBLESHOOTING.md), [privacy](PRIVACY.md), [security reporting](SECURITY.md).

## Requirements and scope

VS Code 1.106+, FFmpeg 6+ and ffprobe on PATH. Web needs the pinned Chromium installed through **Set Up Tools**. Android needs adb, Java 17+, Maestro 2.11, a booted emulator and a single built APK. Linux speech requires espeak; Windows/macOS use local system speech. Restart VS Code after changing tool PATH.

Windows x64, Linux x64 and macOS Intel are the desktop hosts checked. Full Android and Flutter CanvasKit acceptance runs on Windows; project-specific target combinations require validation. iOS, physical devices, split APKs, Flutter desktop, Firefox/WebKit, VS Code Web and ARM host acceptance remain pending. Cloud AI/ElevenLabs are disabled; no cloud account is needed.

Use only trusted projects, reviewed flows, synthetic data and test identities. The Android example clears app data. Captions are selectable subtitles. Videos/screenshots are not anonymized.

Report problems through [issues](https://github.com/gyanupadhyay/releaselens-support/issues) with tool versions and sanitized logs. Report vulnerabilities privately using SECURITY.md. Never attach tokens, auth state or customer recordings.

This public repository provides documentation, support and release binaries. Implementation source remains private.
