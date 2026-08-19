<!-- markdownlint-disable -->

# Hardening Report: skaut--wordpress-version-checker/v2.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **skaut--wordpress-version-checker/v2.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

All 7 `uses:` references in CI.yml are pinned to mutable tags or version strings rather than immutable 40-character SHA commit hashes. This exposes the workflow to supply-chain attacks if any of the referenced actions are compromised or their tags are moved. Failing references: `actions/checkout@v4` (lines 15, 38, 57), `actions/setup-node@v4` (lines 18, 41, 60), `codecov/codecov-action@v4.4.0` (line 70).

Locations:

- `.github/workflows/CI.yml:15`
- `.github/workflows/CI.yml:18`
- `.github/workflows/CI.yml:38`
- `.github/workflows/CI.yml:41`
- `.github/workflows/CI.yml:57`
- `.github/workflows/CI.yml:60`
- `.github/workflows/CI.yml:70`

### missing-permissions (severity: medium)

CI.yml has no top-level `permissions:` key and none of its three jobs (`build`, `lint`, `test`) define a job-level `permissions:` block. The workflow therefore runs with GitHub's default permissions (which include `contents: write` on push events), granting broader access than necessary. A minimal `permissions: read-all` or specific per-job scopes should be added.

Locations:

- `.github/workflows/CI.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed CI.yml: (1) Pinned all 7 `uses:` references to immutable 40-char commit SHAs — actions/checkout@v4 → 34e114876b0b11c390a56381ad16ebd13914f8d5, actions/setup-node@v4 → 49933ea5288caeca8642d1e84afbd3f7d6820020, codecov/codecov-action@v4.4.0 → 6d798873df2b1b8e5846dba6fb86631229fbcb17 — with original tags preserved as inline comments. (2) Added top-level `permissions: contents: read` block to restrict the workflow from running with GitHub's default broad permissions.

