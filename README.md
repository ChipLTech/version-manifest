# ChipLTech Version Manifest

This public repository stores the latest commit manifest used by
`arsenal/check_version.py`.

The manifest intentionally exposes only repository names, default branch names,
latest commit SHAs, and update timestamps. It must not contain source code,
clone URLs, tokens, commit messages, authors, diffs, or file paths.

Machine-readable manifest:

```text
https://raw.githubusercontent.com/ChipLTech/version-manifest/main/check-version/latest.json
```

## Refresh workflow

`.github/workflows/update-version-manifest.yml` refreshes the manifest once per
hour and can also be triggered manually from the Actions tab.

Configure a repository secret named `VERSION_MANIFEST_SOURCE_TOKEN` in this
repository. The token should be a fine-grained PAT for `ChipLTech` with
read-only `Contents` permission on the private source repositories listed in the
workflow. The workflow writes updates back to this public repository with its
built-in `GITHUB_TOKEN`.

## CLsim migration

Track `CLsim` alongside `DLCsim` while Arsenal's current main still reads the
legacy manifest key. Each entry must use that repository's own commit SHA.
Let the refresh workflow update `check-version/latest.json` after the tracking
change is merged; keep generated JSON out of migration PRs.
Before merging the refresh change, grant `VERSION_MANIFEST_SOURCE_TOKEN`
read-only Contents access to `CLsim`. Publish the refreshed manifest containing
`CLsim` before merging Arsenal's consumer migration; retire the `DLCsim` entry
separately after the remaining consumers have switched.
