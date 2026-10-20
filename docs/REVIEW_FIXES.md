# 0.2.1 review resolution

| Finding | Change and verification |
| --- | --- |
| Redirect allowlist bypass | Redirect responses abort before following any hop; real Chromium regression proves forbidden server receives zero requests |
| Caller-controlled Android provenance | GitHub deployment attests APK hash and artifact/run/digest; verifier rejects absent/mismatched attestations, build SHAs and artifact digests |
| Concurrent extension children | Session reserves ownership before secret reads; unit and actual VS Code host concurrency regressions |
| Device-wide recorder termination | Per-device lease and owned PID/output-path check; recorder input regressions and real emulator recording |
| Stale recovery guard | Leased coordinator replaces permanent empty guard; stale lease and legacy guard recovery regressions |
| Windows workflow arguments | Node literal-argument runner replaces shell-dependent environment expansion; cloud-only undeclared secret removed |
| Misleading deployed range | Explicit unverified range label plus project-local verified receipt selection; CLI independently checks receipt |
| Flutter web gap | Flutter semantics selector mode, accessible assertion polling, real release CanvasKit sample and recorded acceptance gate |
| Core/adapter cycle and process boundary | Adapter injection, architecture regression, typed CLI response schemas; extracted credentials/session/webview concerns |
| Incomplete fingerprints | Git file inventory covers all nonignored source bytes including XML/Kotlin/gradlew; mutation regressions |
| Old browser runtime | Playwright 1.64.1 pinned and vendored cleanly; browser setup and third-party notices refreshed |
| Missing public information | Public guide, CI attestation instructions, architecture/trust boundaries, configuration schemas, platform table and public listing repository links |
| Development-only host verification | Exact audited VSIX bytes extracted and exercised in actual VS Code on every CI host; publishing gate binds local host result to archive SHA-256 |

The release procedure requires fresh final-revision evidence. Individual development passes are not substituted for those release checks. Unsupported platforms and disabled cloud services remain explicit in USER_GUIDE.md. Further controller decomposition is a maintainability option, not a claim that an independently supported SDK exists.
