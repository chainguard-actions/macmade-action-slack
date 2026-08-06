<!-- markdownlint-disable -->

# Hardening Report: macmade--action-slack/v1.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **macmade--action-slack/v1.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses `macmade/action-slack@v1.0.0`, which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling supply-chain attacks. It should be replaced with the full SHA, e.g. `macmade/action-slack@<40-hex-char-sha> # v1.0.0`.

Locations:

- `.github/workflows/test.yml:8`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the `test` job also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions (which may be `write-all`). A minimal `permissions:` block should be added to restrict the GITHUB_TOKEN to only the scopes required.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `macmade/action-slack@v1.0.0` to its full commit SHA `946af3142e8b80fba76ba5acae717cb5427b3811` (tag preserved as a comment). 2. Added `permissions: {}` at the top level of the workflow, since the workflow only sends a Slack notification via a webhook secret and requires no GITHUB_TOKEN permissions.

