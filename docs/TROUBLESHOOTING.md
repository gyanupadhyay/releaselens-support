# Troubleshooting

- **PowerShell blocks npm/npx:** use `.cmd` wrappers without changing system execution policy.
- **Chromium missing:** run `npx playwright install chromium` using the pinned runtime. The VSIX installer path is documented in README.
- **FFmpeg missing:** use `scripts/with-media.mjs` for repository development, or install FFmpeg/ffprobe on PATH.
- **Speech fails:** install a system voice or choose explicit silent output; Windows System.Speech may require access outside a restrictive sandbox. Linux needs espeak. A failed speech provider fails the run; use `--silent` explicitly if desired.
- **Android unavailable:** boot an emulator, inspect `adb devices`, and configure its exact serial. APK app ID and Maestro flow header must agree. The adapter does not boot the emulator automatically.
- **Gradle distribution download times out:** the APK build requires access to the distribution URL in `examples/flutter-demo/android/gradle/wrapper/gradle-wrapper.properties` and Android artifact repositories. Restore network/proxy access or pre-provision those caches, then rerun `flutter build apk --debug`. Flutter analysis/widget tests do not verify an APK build.
- **Maestro fails on Windows:** use the documented portable installation and set `RELEASELENS_MAESTRO_HOME` to the extracted directory containing `lib`. Java 17+ must be on PATH. The tool invokes the official Java main class directly; it does not execute `.bat` wrappers through a command shell.
- **Android assertions missing:** registered strings must be direct mandatory `assertVisible` commands. Optional/nested assertions are not eligible for narration.
- **Recording duration exceeded:** split Android flows into scenarios below the 170-second cap.
- **Blocked URL:** review approved origins, route prefixes, asset/API requests and redirects. Avoid arbitrary external origins.
- **Flow failure:** inspect run manifest, per-scenario result, screenshots, Maestro XML and media logs. Partial output requires `--allow-partial` and stays marked partial.
- **GitHub 403/404:** check repository access and token permissions. Release analysis requires full SHAs and a descendant commit range.
- **MP4 preview unavailable:** open the video in an external player; VS Code codec support varies.
- **Interrupted run lock:** run `releaselens recover` only after the prior process exits. It refuses recovery while a project run is alive and marks unfinished results failed.
- **Timed narration filter unavailable:** use FFmpeg 6+; the doctor checks its major version. The current development helper uses ffmpeg-static rather than the obsolete 2018 installer binary.
- **Public release command fails:** inspect `artifacts/release-evidence/release-readiness.json`. Missing owner identity, live acceptance or platform evidence intentionally blocks release approval. See docs/PUBLIC_RELEASE.md.
