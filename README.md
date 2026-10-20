# ReleaseLens AI support

Public documentation and issue tracking for the ReleaseLens AI VS Code extension. The implementation repository remains private.

Marketplace listing: https://marketplace.visualstudio.com/items?itemName=gyanupadhyay.releaselens-ai

The 0.2.0 pre-release records reviewed Android emulator and web scenarios, composes MP4 videos with local system narration and captions, and matches PR metadata to registered scenario tags. Cloud AI planning and ElevenLabs are disabled; no cloud speech or AI account is required. iOS and physical-device farms are not supported.

## Requirements

VS Code 1.106 or newer, FFmpeg 6 or newer, and ffprobe on PATH. Web recording needs pinned Chromium, installed through ReleaseLens: Set Up Tools. Android needs an Android emulator, adb, Java, Maestro, and your built APK. Linux narration needs espeak; Windows and macOS use system speech.

## Getting started

Install the Marketplace pre-release, open a trusted project, and choose ReleaseLens: Initialize Project. Review the generated configuration and flow files for your app ID, APK, URLs and selectors. Check prerequisites using ReleaseLens: Set Up Tools, then choose Plan & generate in the sidebar. Always record synthetic data and test accounts.

## Report a problem

Open an issue with your OS, VS Code and extension versions, target platform, steps to reproduce, and sanitized diagnostics. Never upload API keys, passwords, personal recordings or private source code. Videos and screenshots are not automatically anonymized. See PRIVACY.md.
