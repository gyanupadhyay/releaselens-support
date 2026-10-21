# iOS Simulator setup

ReleaseLens 0.3 adds a macOS-only iOS Simulator adapter. It uses Apple's `simctl` to install and record a built app, and Maestro to execute reviewed UI flows. This is local simulator support; physical iPhones, IPA installation and verified iOS deployment receipts are not supported. Android and web remain separate platform adapters.

## Requirements

- A Mac with full Xcode, accepted Xcode license and an installed iOS Simulator runtime. Command Line Tools alone are insufficient. Check `xcodebuild -version` and `xcrun simctl list devices available`.
- Flutter configured for iOS, Java 17+, Maestro 2.11.0, FFmpeg 6+ and ffprobe on PATH. Restart VS Code after updating PATH. The extension uses VS Code's Node runtime; standalone CLI requires Node.js 22+.
- A built **simulator** `.app`. Build your Flutter app with `flutter build ios --simulator --debug --no-codesign`; the usual output is `build/ios/iphonesimulator/Runner.app`. Device-signed IPAs and device-only `.app` builds cannot run in Simulator.

Select `flutter-ios` during **Initialize Project**. Initialization creates config, registry and `.releaselens/flows/ios.yaml` without overwriting files. In existing projects add the iOS config/registry/flow manually. All platforms share the project lock and output format.

```json
{
  "schemaVersion": 1,
  "platform": "flutter-ios",
  "ios": {
    "appPath": "build/ios/iphonesimulator/Runner.app",
    "bundleId": "com.example.yourapp",
    "device": "12345678-1234-1234-1234-123456789ABC"
  },
  "narration": {"provider": "system"},
  "video": {"captions": true, "fps": 30},
  "timeoutSeconds": 170
}
```

Replace the sample UUID with an actual booted iOS simulator from `xcrun simctl list devices booted`. Replace the bundle ID with your app's `CFBundleIdentifier`; the flow's `appId` must match it. Paths must remain inside the project, and app bundles containing symlinks are rejected. `booted` is deliberately not accepted as a device ID because it is ambiguous when multiple simulators run. The extension's generation flow offers a picker of available booted iOS devices.

## Reviewed flow

Register a scenario with `platform: "flutter-ios"`, its project-relative YAML path, tags, prerequisites and mandatory textual assertions. Use stable Flutter Semantics identifiers or accessible text in Maestro. Example:

```yaml
appId: com.example.yourapp
---
- launchApp:
    clearState: true
- extendedWaitUntil:
    visible:
      id: "task-input"
    timeout: 45000
- tapOn:
    id: "task-input"
- inputText: "Release demo task"
- tapOn:
    id: "add-task"
- assertVisible: "Release demo task"
```

`clearState: true` clears the selected app's test data. Review it before execution and use synthetic data. Every registry assertion must appear as a direct mandatory `assertVisible` command. Optional/nested assertions do not authorize narration. First dismiss OS education dialogs deliberately; ReleaseLens does not click arbitrary system prompts or automatically boot/erase devices.

Choose **Set Up Tools → Check tools**, then **Plan & generate demo → flutter-ios → Registered scenarios**. Select reviewed scenarios, the booted simulator and narration/silent output. Mac speech uses `say`. Cancel through the normal progress notification or sidebar.

The adapter checks the `.app`'s bundle ID and Simulator platform, hashes its file paths/bytes, installs it, and verifies the installed `.app` has identical contents. It acquires the simulator's per-user device lease, waits for its own recorder readiness, runs Maestro, and stops only its own `simctl` process. Missing recordings, failed assertions, unsupported evidence, build mismatches and timeouts fail the run and preserve diagnostics. Assertion evidence drives narration timing, as on Android.

## Acceptance and limits

The `iOS Simulator acceptance` workflow builds the real Flutter sample on an isolated macOS Apple Silicon runner, creates a simulator, installs pinned Maestro, and verifies recording, installed bundle hashes, completed assertions and local narration. The public release gate requires successful current-source iOS evidence. See its generated evidence for the actual Xcode/runtime/Flutter versions tested. No live acceptance is claimed from Windows unit tests.

The iOS acceptance target is Apple Silicon; Intel simulator acceptance and complete Apple Silicon packaged-host acceptance remain pending. iOS deployment receipts are rejected explicitly until an authenticated simulator artifact/build attestation is implemented. A PR merge or local `.app` hash is never labeled a verified deployment. This feature belongs to the public pre-release scope.

References: [Apple Simulator recording](https://developer.apple.com/videos/play/wwdc2020/10647/), [Maestro iOS support](https://docs.maestro.dev/get-started/supported-platform/ios).

## Measured 0.3.0 acceptance

Passed on the macOS Apple Silicon CI runner with Flutter 3.47.7, Xcode 16.4, iPhone 16 and iOS 26.2 Simulator. The installed bundle hash matched the source bundle, Maestro observed `Release demo task`, and local speech began after that assertion. The release video is included with the GitHub pre-release. Full Apple Silicon VS Code host and Intel iOS Simulator acceptance remain pending.

[Watch/download the real narrated iOS recording](https://github.com/gyanupadhyay/releaselens-support/releases/download/v0.3.0/releaselens-ios-demo.mp4). The task data is synthetic.
