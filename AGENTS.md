# Konveyor Enhancements

Enhancement tracking and design proposal repository for the [Konveyor](https://www.konveyor.io/) project (CNCF). Inspired by the Kubernetes enhancement process.

Konveyor accelerates application modernization to Kubernetes. This repo is the central place to propose, discuss, and reach consensus on cross-project enhancements via actionable design documents.

## Repository Structure

- `enhancements/` — Enhancement proposals organized by domain (e.g., `crane-2.0/`, `kantra/`, `kai/`, `common/`)
- `guidelines/` — Process docs and the [enhancement template](guidelines/enhancement_template.md)
- `ROADMAP.md` — Community roadmap

Each enhancement lives in `enhancements/<domain>/<slug>/README.md` following the YAML-frontmatter template from `guidelines/enhancement_template.md`.

## Skills

### `/writing-enhancements`

Use when writing a new Konveyor enhancement proposal. Provide a feature description and target domain — the skill generates a complete proposal document following the project template and conventions.
