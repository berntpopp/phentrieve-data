# Phentrieve HPO Data Releases

This repository contains immutable metadata and GitHub Release assets for
Phentrieve HPO vector indexes. It does not contain generated ontology files,
embedding models, SQLite databases, or Chroma indexes in Git.

## Release lifecycle

Phentrieve software is released from
[berntpopp/phentrieve](https://github.com/berntpopp/phentrieve). HPO data is
released here with tags of the form `hpo-vYYYY-MM-DD-rN`.

Each committed JSON file under `releases/` pins:

- the HPO release URL, version, date, and SHA-256 digest;
- the Phentrieve source commit and `uv.lock` SHA-256 digest;
- the Hugging Face commit for every embedding model;
- expected active-term and multi-vector document counts.

The release workflow invokes a full-SHA-pinned reusable workflow from the
software repository on a GPU runner. It creates a draft release only. Assets
are verified before a maintainer publishes the draft.

## Install and verify

Phentrieve defaults to this repository for bundle discovery. For example:

```bash
phentrieve data download --model biolord --multi-vector --hpo-version v2026-06-23
```

To inspect an asset independently, download its matching `SHA256SUMS` file and
verify it before extraction:

```bash
sha256sum --check --ignore-missing SHA256SUMS
```

Historical data releases are mirrored here under their original `data-v...`
tags so existing automation can move to this repository without changing an
asset name. They retain the legacy archive layout and checksum filenames. The
software repository keeps its original releases as read-only compatibility
copies; new data releases are published only here.

## Publication policy

Every release must contain the minimal bundle, one single-vector and one
multi-vector bundle for each declared model, `SHA256SUMS`,
`release-manifest.json`, and `verification-report.json`. Publish immutable
releases only after the full artifact set and remote checksums have been
reviewed.

Historical mirrors predate this contract. Their original GitHub Release
metadata and assets are preserved, and their GitHub-provided SHA-256 digests
are compared with the source release before publication.
