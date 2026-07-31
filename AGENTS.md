# Konveyor Enhancements

Enhancement tracking and design proposal repository for the [Konveyor](https://www.konveyor.io/) project (CNCF). Inspired by the Kubernetes enhancement process.

Konveyor accelerates application modernization to Kubernetes. This repo is the central place to propose, discuss, and reach consensus on cross-project enhancements via actionable design documents.

## Repository Structure

- `enhancements/` — Enhancement proposals organized by domain (e.g., `crane-2.0/`, `kantra/`, `kai/`, `common/`)
- `guidelines/` — Process docs and the [enhancement template](guidelines/enhancement_template.md)
- `ROADMAP.md` — Community roadmap

Each enhancement lives in `enhancements/<domain>/<slug>/README.md` following the YAML-frontmatter template from `guidelines/enhancement_template.md`.

## Writing an Enhancement Proposal

When asked to write an enhancement, follow this process:

1. **Validate working directory** — confirm `enhancements/` and `guidelines/` directories exist. If not, stop and tell the user to run from their enhancements repo fork.
2. **Get required input** — feature description and target domain (subdirectory under `enhancements/`). If domain is not provided, list existing ones with `ls enhancements/`.
3. **Derive metadata:**
   - **Slug:** kebab-case from the feature description (e.g., `multi-stage-kustomize-transforms`)
   - **Author:** from `git config user.name` / `git config user.email`
   - **Date:** today's date (`yyyy-mm-dd`)
   - **Status:** always `provisional` for new proposals
4. **Generate the document** at `enhancements/<domain>/<slug>/README.md` using the template from [guidelines/enhancement_template.md](guidelines/enhancement_template.md). Fill every section from the user's input — do not leave TBD/TODO. If input doesn't cover a section, infer and mark with `<!-- REVIEW: inferred, please verify -->`.
5. **Completeness check** — verify all sections present, YAML frontmatter valid, no unintentional placeholders, directory name matches `title` field. Report the file path and any sections marked for review.

### Conventions

- Directory names: lowercase kebab-case
- Each enhancement in its own directory: `enhancements/<domain>/<slug>/`
- The proposal file is always `README.md`
- Images or supporting assets go in the same directory
- The YAML `title` field matches the directory name (the slug)
