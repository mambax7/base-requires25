# XOOPS Copilot Instructions — base-requires25

## About This Repository

**base-requires25** is a Composer metapackage (contains no code) that defines the primary PHP dependencies for [XOOPS/XoopsCore25](https://github.com/XOOPS/XoopsCore25). It separates core requirements from module-level requirements that may be added to the main `composer.json`.

- **Upstream:** https://github.com/XOOPS/base-requires25
- **Issues:** https://github.com/XOOPS/XoopsCore25/issues
- **License:** GPL-2.0-or-later

## Project Layout

```
composer.json                    # The sole deliverable — defines all dependencies
LICENSE                          # GPL-2.0
README.md                        # Usage instructions
.github/
  copilot-instructions.md        # This file
  CONTRIBUTING.md                # Contribution guidelines
  ISSUE_TEMPLATE/                # Bug report / feature request templates
```

This is a **metapackage** — it contains no PHP source code, no classes, no templates. The only file that receives functional edits is `composer.json`.

## Build & Test

Since this is a metapackage with no code, "testing" means validating the dependency manifest:

```bash
composer validate                                           # Validate composer.json syntax and schema
composer update xoops/base-requires25 --dry-run --with-dependencies  # Preview dependency resolution
composer update xoops/base-requires25 --with-dependencies            # Install/update dependencies
```

There are no PHPUnit tests, no linting, and no code style checks — there is no code to check.

## PHP Compatibility

The metapackage must declare a PHP version constraint that covers **PHP 7.4 through PHP 8.5**. The correct Composer constraint for this is:

```json
"php": "^7.4 || ^8.0"
```

- `^7.4` covers `>=7.4.0, <8.0.0` (i.e., PHP 7.4.x)
- `^8.0` covers `>=8.0.0, <9.0.0` (i.e., PHP 8.0 through 8.x)

All listed dependencies must themselves support this PHP range or have polyfills where needed.

## Composer Metapackage Conventions

- **Type must be `metapackage`** — this tells Composer there are no files to install.
- **Use caret (`^`) version constraints** for maximum interoperability (e.g., `^4.19`, not `~4.19.0` or `>=4.19`).
- **Keep `sort-packages: true`** — packages in `require` must be in alphabetical order.
- **Prefer inline stability flags** over global `minimum-stability`. Instead of setting `"minimum-stability": "beta"` globally, use `@beta` on specific packages that need it:
  ```json
  "xoops/xmf": "^1.2.33-beta2@beta"
  ```
- **Use `preferred-install: dist`** — download zip archives instead of cloning repos.
- **Follow Semantic Versioning** — version bumps in this metapackage should reflect the impact of dependency changes.

## Dependency Management Guidelines

When updating `composer.json`:

1. **Verify PHP compatibility** — ensure the new version of a dependency supports PHP 7.4 through 8.5.
2. **Check for breaking changes** — read the dependency's changelog before bumping a major version.
3. **Validate after changes** — always run `composer validate` after editing `composer.json`.
4. **Test resolution** — run `composer update --dry-run --with-dependencies` to confirm all dependencies resolve without conflicts.
5. **Keep constraints as loose as practical** — use `^major.minor` not `^major.minor.patch` unless a specific patch is required.
6. **Watch for abandoned packages** — check Packagist for deprecation/abandonment notices before relying on a package.

## Current Dependency Overview

| Package | Role | Status |
|---|---|---|
| `xoops/xmf` | XOOPS Module Framework | Active, beta |
| `xoops/regdom` | Domain registration utilities | Active, beta |
| `ezyang/htmlpurifier` | HTML sanitization | Active |
| `phpmailer/phpmailer` | Email sending (6.x branch) | Active |
| `smarty/smarty` | Template engine (v4, final release) | Maintenance-only |
| `tecnickcom/tcpdf` | PDF generation | Support-only mode |
| `smottt/wideimage` | Image processing (GD) | Abandoned |
| `boenrobot/money_format_polyfill` | money_format() polyfill | Abandoned |
| `symfony/polyfill-iconv` | iconv polyfill | Active |
| `symfony/polyfill-mbstring` | mbstring polyfill | Active |

## Security Practices

Even though this repo has no code, dependency choices affect security:

- Prefer packages with active security advisories and responsive maintainers.
- Monitor Packagist and GitHub Security Advisories for CVEs in listed packages.
- Pin to versions that include known security fixes (e.g., HTMLPurifier 4.19+ for backtracking fix).
- Avoid abandoned packages that will never receive security patches.

## Pull Request Checklist

1. `composer.json` passes `composer validate` with no warnings.
2. All dependencies resolve without conflicts (`composer update --dry-run --with-dependencies`).
3. PHP version constraint covers 7.4 through 8.5 (`"php": "^7.4 || ^8.0"`).
4. No abandoned or unmaintained packages added without justification.
5. Version constraints use caret notation and are as loose as safely possible.
6. Packages in `require` are alphabetically sorted.
7. Changes are documented in commit messages (which package, from/to version, why).
8. No `minimum-stability: beta` — use inline `@beta` flags on specific packages instead.
