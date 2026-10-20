# CLI and CI setup

Public users can use the CLI bundled in the installed extension without cloning the private implementation repository. In a VS Code terminal, locate it with `code --locate-extension gyanupadhyay.releaselens-ai`. With Node.js 22+ and the documented external tools on PATH:

```sh
node /absolute/extension/path/dist/cli.mjs --help
node /absolute/extension/path/dist/cli.mjs doctor --root /absolute/project --platform web --json
node /absolute/extension/path/dist/cli.mjs plan --root /absolute/project --scenario create-task --json
node /absolute/extension/path/dist/cli.mjs run --root /absolute/project --scenario create-task --silent --json
```

On Windows quote paths with spaces; use forward slashes or native absolute paths. For headless CI, download the versioned VSIX and checksum from this repository Releases, verify SHA-256, extract it as ZIP, and invoke `extension/dist/cli.mjs` from the extracted directory with Node.js 22+. Install the pinned browser using `node /absolute/extension/path/dist/cli.mjs setup --browser`; provision Linux browser dependencies separately. Use scoped environment credentials and trusted default-branch flows.

The source-owner reusable workflow below is a reference template, not a publicly callable workflow URL. Public consumers can implement their own pipeline around the distributed CLI. For a verified run, create a project-local receipt after deployment and smoke checks:

```json
{"schemaVersion":1,"repository":"owner/repo","deployedSha":"<full SHA>","previousSha":"<full SHA>","deploymentId":"<numeric ID>","smokeCheck":"staging-smoke","checkedAt":"<current ISO timestamp>"}
```

Supply `GITHUB_TOKEN` with read permissions described below and run `node /absolute/extension/path/dist/cli.mjs run --root /absolute/project --scenario create-task --deployment-receipt deployment-receipt.json --json`. Receipts expire after 24 hours. The CLI independently verifies GitHub and the running target. Android receipts additionally require `apkSha256` and `androidArtifact: {"runId":"...","artifactId":"...","digest":"..."}` matching the trusted server-side payload described below. Never accept unreviewed PR receipt values as pipeline attestations.

## Source-owner integration template

The reusable workflow is an integration template. The release gate separately exercises a real transient GitHub deployment and running web sample; adapt and validate this workflow against your deployment system before using it.

1. Commit reviewed config, registry and flows to the trusted default branch.
2. Configure repository, staging URL, `web.releasePath` and allowed origins. The version endpoint must return `{ "commitSha": "<full deployed SHA>" }`. On hosted Linux the workflow provisions espeak for local system narration. Cloud speech is disabled in this pre-release.
3. Have your deployment pipeline create a GitHub Deployment for the actual SHA and publish a successful status after rollout.
4. Publish a smoke-test GitHub check run on that SHA. The gate expects a check run, not a legacy commit status.
5. Read the previous successfully deployed SHA from your deployment system. Do not infer it from the previous PR.
6. Call the reusable workflow after deployment and smoke jobs pass. The demo job has read-only GitHub permissions and checks out trusted automation from the default branch.

Example caller job; adapt output names to your pipeline:

```yaml
release-demo:
  needs: [deploy, smoke]
  if: needs.deploy.result == 'success' && needs.smoke.result == 'success'
  uses: ./.github/workflows/release-demo.yml
  with:
    deployment-id: ${{ needs.deploy.outputs.deployment_id }}
    deployed-sha: ${{ needs.deploy.outputs.deployed_sha }}
    previous-sha: ${{ needs.deploy.outputs.previous_sha }}
    smoke-check-name: staging-smoke
    scenario: web-add-task
    platform: web
    web-url: https://staging.example.com
```

The caller must permit `contents: read`, `deployments: read`, `checks: read`, and `actions: read`. Scope write permissions required by deployment/check publishing to earlier jobs.

For Android, select a prepared runner via `runner`, install Maestro/adb and boot its emulator. Pass `apk-run-id`, `apk-artifact` and `apk-sha256` from the deployment pipeline. When the trusted deployment-writing job creates the GitHub Deployment, include this payload (strings shown as placeholders):

```json
{"releaselens":{"apkSha256":"<64 hex APK hash>","runId":"<successful build run ID>","artifactId":"<uploaded artifact ID>","digest":"<64 hex artifact ZIP digest, without sha256:>"}}
```

Use the build upload action's artifact ID/digest and compute the APK hash before upload. The deployment-writing pipeline is the trust boundary: it must attest the artifact actually deployed, and must not accept unreviewed PR values for these fields. The read-only demo job independently checks the server-side attestation, successful same-repository run SHA, unexpired artifact/run association and GitHub artifact digest. A pinned action downloads the authenticated artifact by ID; exactly one APK is selected and hashed before installation, then the installed app's hash is checked too. Legacy Android receipts without this attestation are rejected and must be regenerated. Automatic emulator provisioning is not included. The Node runner passes arguments literally on Windows and POSIX hosts.

The gate writes a versioned `deployment-receipt.json`. Generation consumes it with `--deployment-receipt`, rechecks GitHub, and verifies the running web SHA or APK hash. A caller flag alone cannot set verified provenance. Artifacts upload even on failure for diagnostics; upload does not imply success. Videos are not attached to a public release. Live execution remains an external release gate until your repository and credentials are configured.
