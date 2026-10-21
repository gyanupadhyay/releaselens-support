# Changelog

## 0.3.0

- Add macOS iOS Simulator adapter: install a simulator .app, verify installed bundle contents, capture simctl video and collect Maestro assertion evidence.
- Add iOS initialization, configuration schemas, simulator discovery/picker, diagnostics, cancellation, per-device leases and an isolated real iOS CI acceptance gate.
- iOS supports local simulator demos; iOS deployment receipts, physical iPhones and Windows/Linux execution remain unsupported.
- iOS requires macOS, Xcode with an installed iOS runtime, Java/Maestro and a prebuilt simulator .app. Read the iOS setup guide.


## 0.2.1

- Block HTTP redirect chains before following a destination outside the reviewed request policy. Configure final URLs; redirects are unsupported.
- Bind Android receipts to authenticated deployment/build/artifact attestations; reject legacy unattested receipts.
- Reserve extension command ownership before asynchronous work, freeze workspace selection and validate CLI responses.
- Add per-device leases, owned recorder PID checks and crash-recoverable coordinator locks.
- Decouple the core engine from platform adapters and extract session, credentials and webview concerns.
- Add real Flutter web semantics recording, configuration editor schemas, verified-receipt selection and recovery UI.
- Upgrade pinned Playwright to 1.64.1; install the new Chromium revision through Set Up Tools.
- Expand source fingerprint coverage and run real-host checks against packaged VSIX bytes on all three host operating systems.
- Publish complete onboarding, flow, provenance, privacy, output, recovery and platform guides through the public support repository.


## 0.2.0

- Added cancellable generation, subprocess tree cleanup, project run locks and interrupted-run recovery.
- Added setup diagnostics, explicit pinned browser installation, generation history and emulator selection.
- Initialization now writes its example flow files and refuses to overwrite existing project configuration.
- Added actual VS Code extension-host tests for command activation, initialization, diagnostics, recording, preview, history and cancellation.
- Added bounded GitHub retries/diff evidence, strict deployment receipts, deployed web SHA checks and APK hash verification.
- Added per-assertion speech files, evidence-derived narration timing and aligned captions.
- Added source-revision release evidence, cross-platform CI and a publishing gate requiring owner identity and external acceptance.
- Android and web are the supported targets. iOS is not implemented.
### Public pre-release scope

Android/web recording, local system narration, captions, deterministic scenario matching, and verified GitHub deployments. Cloud AI and ElevenLabs are disabled; no cloud API key is required. Public support: https://github.com/gyanupadhyay/releaselens-support/issues.
