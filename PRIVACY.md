# Privacy and data handling

ReleaseLens stores configuration and generated artifacts in your selected local workspace. Recordings can contain everything visible in the test app. Use synthetic fixtures and test accounts; screenshots and videos are not automatically anonymized.

- GitHub: when you request PR/release analysis or deployment verification, ReleaseLens sends authenticated requests to api.github.com and retrieves metadata, changed filenames and bounded diff patches.
- AI: cloud AI planning is disabled in this pre-release. Scenario suggestions use deterministic tag matching. No data is sent to an AI service.
- Speech: narration uses your local system voice. Cloud speech and ElevenLabs are disabled in this pre-release.
- Tool setup: explicit Chromium installation downloads the pinned Playwright browser. Other tools are installed by you. ReleaseLens disables Maestro CLI analytics in subprocesses it launches.
- Credentials: the extension stores your GitHub token using VS Code SecretStorage. CLI/CI credentials come from environment variables. Known environment secrets and sensitive JSON fields are redacted from textual diagnostics. This cannot remove sensitive information displayed in media, or unknown secrets embedded in arbitrary application output.
- Telemetry: ReleaseLens does not collect its own usage telemetry. Network activity of VS Code and other independently installed applications is governed by their settings and policies.

You control artifact retention. Local output is not uploaded automatically. The supplied GitHub workflow uploads diagnostic/video artifacts to your repository's Actions storage with a seven-day retention setting. Failure artifacts may contain screenshots and logs; restrict repository/artifact access accordingly.

Remove a key by choosing its credential command and submitting an empty value. Delete local artifacts when no longer needed. Uninstalling the extension does not remove workspace configuration or recordings.
