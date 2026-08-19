<!-- markdownlint-disable -->

# Hardening Report: skaut--wordpress-version-checker/v2.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **skaut--wordpress-version-checker/v2.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

CI.yml uses mutable tag/version references instead of pinned SHA commits, making the workflow vulnerable to supply-chain attacks if the referenced action tags are moved or compromised. Failing references: actions/checkout@v4 (used 3 times), actions/cache@v4 (used 3 times), codecov/codecov-action@v4.4.0 (used 1 time). All should be pinned to full 40-character commit SHAs.

Locations:

- `.github/workflows/CI.yml:14`
- `.github/workflows/CI.yml:17`
- `.github/workflows/CI.yml:33`
- `.github/workflows/CI.yml:36`
- `.github/workflows/CI.yml:52`
- `.github/workflows/CI.yml:55`
- `.github/workflows/CI.yml:71`

### missing-permissions (severity: medium)

CI.yml has no top-level permissions: key and none of its three jobs (build, lint, test) define job-level permissions. Without explicit permissions, the workflow inherits the default repository permissions, which may be overly broad (e.g. write access to contents). A minimal permissions block such as 'permissions: read-all' or specific scopes should be added.

Locations:

- `.github/workflows/CI.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed CI.yml: (1) Pinned all 7 action references to full commit SHAs — actions/checkout@v4 → 34e114876b0b11c390a56381ad16ebd13914f8d5, actions/cache@v4 → 0057852bfaa89a56745cba8c7296529d2fc39830, codecov/codecov-action@v4.4.0 → 6d798873df2b1b8e5846dba6fb86631229fbcb17 — with original tags preserved as inline comments. (2) Added top-level `permissions: contents: read` block to restrict the workflow to the minimum permissions needed (read-only repository contents for checkout).

