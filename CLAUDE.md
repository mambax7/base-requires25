# CLAUDE.md - Project Guide for AI Assistants

## Project Overview

**xoops/base-requires25** is a Composer metapackage (no code) that defines the primary PHP dependencies for [XOOPS/XoopsCore25](https://github.com/XOOPS/XoopsCore25). It separates core requirements from module-level requirements in the main `composer.json`.

- **Type:** Composer metapackage
- **License:** GPL-2.0-or-later
- **PHP:** ^7.4 || ^8.0 (targets 7.4 through 8.5)
- **Upstream:** https://github.com/XOOPS/base-requires25
- **Fork:** https://github.com/mambax7/base-requires25

## Repository Structure

```
composer.json                    # The sole deliverable — defines all dependencies
LICENSE                          # GPL-2.0
README.md                        # Usage instructions
CLAUDE.md                        # This file
.gitattributes                   # Line endings and export-ignore rules
.gitignore                       # Ignored files (vendor/, .idea/, etc.)
.scrutinizer.yml                 # Scrutinizer CI — validates composer.json
.github/
  copilot-instructions.md        # GitHub Copilot / AI context
  CONTRIBUTING.md                # Contribution guidelines
  ISSUE_TEMPLATE/                # Bug report / feature request templates
docs/
  tasks.md                       # Improvement task tracker
```

This repo has no PHP source code. All changes are to `composer.json`.

## Key Dependencies

| Package | Purpose | Status |
|---|---|---|
| xoops/xmf | XOOPS Module Framework | Active (beta) |
| xoops/regdom | Domain registration utilities | Active (beta) |
| ezyang/htmlpurifier | HTML sanitization | Active |
| phpmailer/phpmailer | Email sending (6.x) | Active |
| smarty/smarty | Template engine (v4) | Final release, Smarty 5 available |
| tecnickcom/tcpdf | PDF generation | Support-only mode |
| smottt/wideimage | Image processing (GD) | Abandoned |
| boenrobot/money_format_polyfill | money_format() polyfill | Abandoned |
| symfony/polyfill-iconv | iconv polyfill | Active |
| symfony/polyfill-mbstring | mbstring polyfill | Active |

## Known Issues

- `smottt/wideimage` is abandoned with no PHP 8.1+ support — migration to `intervention/image` planned
- `boenrobot/money_format_polyfill` polyfills a function removed in PHP 8.0 — evaluate if still needed
- `tecnickcom/tcpdf` is in support-only mode, successor `tc-lib-pdf` not yet at feature parity
- Smarty 4.5.6 is the final 4.x release — Smarty 5 migration is a future project (blocked by `conflict` rule)

## Composer Conventions

- **`minimum-stability: stable`** — global stability is `stable`; beta packages use inline `@beta` flags
- **`sort-packages: true`** — packages in `require` are alphabetically ordered
- **`preferred-install: dist`** — download zip archives, not git clones
- **Caret constraints** — use `^major.minor` notation (e.g., `^4.18`, not `^4.18.0`)
- **`conflict` rules** — `smarty/smarty >=5.0` is blocked until XOOPS core migrates
- **`suggest`** — optional extensions (`ext-intl`, `ext-imagick`) are documented

## Workflow

### Branches
- `master` — main/default branch (PRs target here)
- `feature/*` — feature branches for changes

### Making Changes
1. The only file typically edited is `composer.json`
2. Ensure `sort-packages: true` is respected (packages alphabetically ordered in `require`)
3. Use caret (`^`) version constraints (e.g., `^4.19`)
4. Always run `composer validate --strict` after editing

### Testing Changes
```bash
composer validate --strict                                  # Validate syntax (strict)
composer update --dry-run --with-dependencies               # Preview resolution
composer update xoops/base-requires25 --with-dependencies   # Apply updates
```

## File Standards (aligned with XMF & RegDom)

This repo follows the same file conventions as `xoops/xmf` and `xoops/regdom`:

| File | Purpose | Aligned with XMF/RegDom |
|---|---|---|
| `.gitattributes` | LF normalization, export-ignore for dist | Yes |
| `.gitignore` | Excludes vendor/, .idea/, build/, lock files | Yes |
| `.scrutinizer.yml` | CI validation (composer validate) | Yes (adapted for metapackage) |
| `.github/copilot-instructions.md` | AI coding assistant context | Yes (adapted for metapackage) |
| `.github/CONTRIBUTING.md` | Contribution guidelines | Yes (correct repo URL) |
| `.github/ISSUE_TEMPLATE/bug-report.yml` | Bug report with PHP 7.4–8.5 dropdown | Yes |
| `.github/ISSUE_TEMPLATE/feature-request.yml` | Feature request (metapackage wording) | Yes |
| `composer.json` | keywords, funding, suggest, conflict sections | Yes |

## Conventions
- Commit messages are short and descriptive (e.g., "update composer", "XMF 1.2.32")
- PRs go from `mambax7/base-requires25` fork to `XOOPS/base-requires25` upstream
- Keep `composer.lock` out of version control (listed in `.gitignore`)
- See `docs/tasks.md` for the full improvement roadmap
