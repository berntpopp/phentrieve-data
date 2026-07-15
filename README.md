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

The legacy `data-v2026-02-16` release remains in the software repository and
can be selected with `PHENTRIEVE_DATA_RELEASE_REPOSITORY=berntpopp/phentrieve`.

## Publication policy

Every release must contain the minimal bundle, one single-vector and one
multi-vector bundle for each declared model, `SHA256SUMS`,
`release-manifest.json`, and `verification-report.json`. Publish immutable
releases only after the full artifact set and remote checksums have been
reviewed.
