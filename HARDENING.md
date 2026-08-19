<!-- markdownlint-disable -->

# Hardening Report: skaut--wordpress-version-checker/v2.2.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **skaut--wordpress-version-checker/v2.2.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple `uses:` references in CI.yml are pinned to mutable tags/versions rather than immutable 40-character commit SHAs. This exposes the workflow to supply-chain attacks if the upstream action tag is moved or compromised. Failing references: `actions/checkout@v4` (lines 15, 38, 57), `actions/setup-node@v4` (lines 18, 41, 60), `codecov/codecov-action@v5.3.1` (line 72). Each should be replaced with its full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/CI.yml:15`
- `.github/workflows/CI.yml:18`
- `.github/workflows/CI.yml:38`
- `.github/workflows/CI.yml:41`
- `.github/workflows/CI.yml:57`
- `.github/workflows/CI.yml:60`
- `.github/workflows/CI.yml:72`

### missing-permissions (severity: medium)

CI.yml has no top-level `permissions:` key and none of its three jobs (`build`, `lint`, `test`) define a `permissions:` block. Without explicit permissions, the workflow runs with the default token permissions, which may be overly broad (e.g. write access to contents and packages). A minimal `permissions: {}` or specific scopes (e.g. `contents: read`) should be added at the top level or per job.

Locations:

- `.github/workflows/CI.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed CI.yml: (1) Pinned all 7 `uses:` references to full 40-character commit SHAs — actions/checkout@v4 → @34e114876b0b11c390a56381ad16ebd13914f8d5, actions/setup-node@v4 → @49933ea5288caeca8642d1e84afbd3f7d6820020, codecov/codecov-action@v5.3.1 → @13ce06bfc6bbe3ecf90edbbf1bc32fe5978ca1d3 — with the original tag preserved as an inline comment. (2) Added a top-level `permissions: contents: read` block to restrict the GITHUB_TOKEN to the minimum required scope (read-only repository contents for checkout).

