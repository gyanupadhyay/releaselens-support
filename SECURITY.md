# Security policy

Report vulnerabilities through [private security reporting](https://github.com/gyanupadhyay/releaselens-support/security/advisories/new) in the public support repository. The implementation repository is private.

Report suspected credential disclosure privately; do not paste credentials, proprietary diffs, screenshots or customer data into public issues. Public release identity/support metadata is enforced by the release gate.

Security boundaries: reviewed local scenarios are trusted repository code. AI suggestions and PR text do not authorize commands or selectors. Workspace trust is required in VS Code. URL/path validation, restricted command arguments, secrets storage, textual redaction, bounded timeouts and deployment provenance reduce risk but do not sandbox a malicious trusted scenario or anonymize application media.

Security fixes target the latest published version. Use synthetic data for all demonstrations. Runtime npm dependencies and packaged files must pass the release audit. FFmpeg, Android SDK, Java, Maestro and browser binaries are external tools and should be kept updated by the operator.
