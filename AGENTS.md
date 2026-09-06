# AGENTS.md — Agent Instructions for Docupedia

This file is the authoritative guide for any AI agent (Claude, GitHub Copilot, etc.)
working in this repository. Read it in full before making any changes.

---

## What this repository is

Docupedia is a **personal reference repository** of Information Security and Privacy
standards. It contains:

- Plain-English summaries of what each standard requires
- Clause-by-clause breakdowns for study and reference
- Metadata about each standard's current edition, amendments, and ISO catalogue link
- Links to licensed source documents stored in Google Drive
- Transition notes between major editions

It is **not** a policy repository, a compliance evidence store, or a certification tool.
It is one person's structured notes on the standards landscape.

---

## Two-system design

This repo works alongside a Google Drive folder. Each system has a distinct role:

| System | Holds | Why |
|---|---|---|
| **This GitHub repo** | Markdown notes, summaries, clause breakdowns, AGENTS.md | Git versions text well; diffs are readable |
| **Google Drive** | Purchased ISO PDFs, working documents, binaries | Drive handles files Git cannot diff usefully |

**Root Drive folder:** [https://drive.google.com/drive/folders/1CM4qRAFE8jjKRjMPfpenXAb7OvsTWzkl](https://drive.google.com/drive/folders/1CM4qRAFE8jjKRjMPfpenXAb7OvsTWzkl)

Every standard's `source.md` contains a `Licensed documents` row linking to Drive.
When adding a new standard, add its purchased PDF to Drive and update `source.md` accordingly.
Never copy the PDF content into this repo.

---

## What is in scope

- ISO/IEC 27000-series standards (ISMS family)
- Related certifiable standards: ISO/IEC 27701 (PIMS), ISO/IEC 42001 (AI MS)
- Adjacent frameworks referenced alongside ISO standards: NIST CSF, DPDP Act 2023, GDPR
- Transition notes between editions of the same standard
- Mapping files that cross-reference controls across standards

## What is out of scope

- Actual policies or procedures (these belong in a separate repo)
- Compliance evidence, audit logs, or records of any kind
- Personal data of any kind
- Official ISO document text — these are copyrighted; do not reproduce clauses verbatim
- PDFs, Word documents, or any binary files — these go in Google Drive

---

## Folder structure

```
standards/
  iso-{number}/
    README.md              # Required. Rendered on folder click. What the standard is,
                           # scope, current edition, key relationships, certification status.
    source.md              # Required. Edition, amendment, ISO catalogue URL, Drive link.
                           # Never the document content itself.
    clauses/               # One file per clause, named {nn}-{slug}.md
    annex-a/               # For 27001: one file per Annex A theme (a5, a6, a7, a8)
    controls/              # For 27002: one file per control theme or individual control
    transitions/           # Edition-to-edition change summaries, named {old}-to-{new}.md
```

### Naming conventions

| Thing | Convention | Example |
|---|---|---|
| Standard folder | `iso-{number}` lowercase, hyphenated | `iso-27001` |
| Clause file | `{nn}-{slug}.md`, zero-padded | `06-planning.md` |
| Transition file | `{year}-to-{year}.md` | `2013-to-2022.md` |
| Annex A file | `a{n}-{theme}.md` | `a5-organizational.md` |
| New standard | Follow the pattern above | `iso-42001/` |

---

## How to add a new standard

1. Create `standards/iso-{number}/` with at minimum `README.md` and `source.md`.
2. `README.md` must cover: what the standard is, who it applies to, current edition,
   certifiable or guidance only, key relationships to other standards, ISO catalogue URL.
3. `source.md` must cover: full title, edition, committee, ISO catalogue link,
   and a `Licensed documents` row linking to the Drive folder. Never actual document content.
4. Add a row to the root `README.md` standards table.
5. Create sub-folders (`clauses/`, etc.) with `.gitkeep` if empty.
6. Commit message: `feat: add iso-{number} skeleton`

## How to add or update clause notes

1. One file per clause under `clauses/`. Do not combine multiple clauses in one file.
2. File name: `{nn}-{slug}.md` where `nn` is the clause number zero-padded to two digits.
3. Structure each file as: H1 = clause title, H2 = sub-clause, notes in plain English below.
4. Highlight mandatory documented information outputs — these matter most for audit readiness.
5. Note any differences introduced by amendments inline (e.g. **Amd 1:2024 addition:**).
6. Commit message: `docs: add clause {n} notes for iso-{number}`

## How to update a standard's edition

1. Update `source.md` with the new edition and date.
2. Update `README.md` with the new edition.
3. Create a transition file under `transitions/{old}-to-{new}.md` summarising what changed.
4. Update the root `README.md` standards table.
5. Do not delete old clause files — update them in place; Git history holds the prior content.
6. Commit message: `chore: update iso-{number} to {year} edition`

---

## Writing style

- **Plain English first.** The goal is to understand what a standard requires, not to
  reproduce its formal language. Write as you would explain it to a colleague.
- **Be precise about mandatory vs guidance.** ISO uses "shall" for requirements and
  "should" for recommendations. Reflect this — "must document" vs "recommended to".
- **Short sentences.** Each point on its own line where it aids readability.
- **No jargon without explanation.** Define acronyms on first use per file (e.g. ISMS,
  PII, SoA).
- **No reproduced standard text.** Paraphrase and summarise; never quote clauses at length.
  ISO documents are copyrighted.
- **Tables for lists of controls or clauses.** Prose for explanation and context.

---

## What never to commit

| Never commit | Reason |
|---|---|
| Official ISO PDFs or document text | Copyright — ISO sells these; store in Drive instead |
| Personal data of any kind | Privacy |
| Credentials, tokens, or API keys | Security |
| Binary files (Word, Excel, images) | Git cannot diff them usefully; store in Drive instead |
| Compliance evidence or audit records | Wrong repo — belongs in a DMS |
| Policies or procedures | Wrong repo — belongs in a policy repo |

If you find any of the above already committed, flag it in a commit message and
remove it — do not silently leave it in place.

---

## Commit message conventions

```
feat: add iso-{number} skeleton
docs: add clause {n} notes for iso-{number}
docs: expand annex-a {theme} for iso-27001
chore: update iso-{number} to {year} edition
chore: update source.md for iso-{number} amendment
fix: correct clause {n} reference in iso-{number}
```

Keep commit messages under 72 characters. Use the imperative mood ("add", not "added").

---

## Things to check before committing

- [ ] `README.md` exists in every standard folder
- [ ] `source.md` exists in every standard folder with a Drive link
- [ ] Root `README.md` standards table is up to date
- [ ] No binary files or PDFs added (use Drive instead)
- [ ] No ISO document text reproduced verbatim
- [ ] Clause files follow the `{nn}-{slug}.md` naming pattern
- [ ] Commit message follows conventions above

---

## Current standards in this repo

| Folder | Standard | Edition | Status |
|---|---|---|---|
| `iso-27001` | ISO/IEC 27001 — ISMS Requirements | 2022 + Amd 1:2024 | Clauses 4–10 complete, Annex A populated |
| `iso-27002` | ISO/IEC 27002 — Information Security Controls | 2022 | Skeleton only |
| `iso-27005` | ISO/IEC 27005 — Risk Management | 2022 | Skeleton only |
| `iso-27701` | ISO/IEC 27701 — PIMS | 2025 | Skeleton only |

Standards to add next (suggestions): ISO/IEC 27003, ISO/IEC 27004, ISO/IEC 42001, NIST CSF 2.0, DPDP Act 2023.
