# base-requires25 — Improvement Tasks

Generated: 2026-02-07 | Updated: 2026-02-07
PHP target: 7.4 through 8.5 | Smarty: 4.x (with 5.x migration planned)

---

## 1. Critical Fixes (composer.json bugs)

- [x] 1.1 **Fix PHP version constraint** — Changed `"^7.4.0 || ^8.5.0"` to `"^7.4 || ^8.0"` to cover PHP 7.4.x through all 8.x versions. The old constraint excluded PHP 8.0–8.4 entirely.

## 2. Dependency Version Updates

- [ ] 2.1 **Update `ezyang/htmlpurifier` from `^4.18` to `^4.19`** — v4.19.0 (Oct 2025) adds PHP 8.4/8.5 support and fixes a catastrophic backtracking bug in `Core.AggressivelyFixLt`. The `^4.18` constraint does allow 4.19, but bumping the floor ensures installations always get the PHP 8.4+ fixes.
- [ ] 2.2 **Evaluate PHPMailer 7.x migration** — PHPMailer v7.0 (Oct 2025) introduces a BC break: `lang()`, `setLanguage()`, and `$language` are now static. Audit XOOPS core usage of these methods. If no direct usage, consider bumping to `^6.10 || ^7.0`. If affected, document the migration path and defer.

## 3. Stability & Constraint Improvements

- [x] 3.1 **Replace global `minimum-stability: beta` with inline stability flags** — Changed to `minimum-stability: stable` with `@beta` flags on `xoops/xmf` and `xoops/regdom`. Prevents accidentally pulling beta versions of transitive dependencies.
- [x] 3.2 **Normalize constraint notation** — Removed trailing `.0` from version constraints. Changed `"^1.0.2"` to `"^1.0"`, `"^1.33.0"` to `"^1.33"`, etc. Caret semantics are identical but shorter forms are conventional.
- [ ] 3.3 **Add `composer validate` to CI** — If GitHub Actions are introduced (see section 7), add `composer validate --strict` as a check on every PR to catch schema errors automatically.

## 4. Abandoned Dependency Remediation

- [ ] 4.1 **Plan replacement for `smottt/wideimage`** — Package is abandoned (last release: Jan 2021, marked "Last v1 release"). No PHP 8.1+ support. Evaluate alternatives: (a) `intervention/image` v3 (most popular, GD/Imagick/libvips), (b) `imagine/imagine` (OOP, GD/Imagick/Gmagick). This requires changes in XOOPS core, not just this metapackage. Create a tracking issue in XoopsCore25.
- [ ] 4.2 **Evaluate necessity of `boenrobot/money_format_polyfill`** — `money_format()` was deprecated in PHP 7.4 and removed in PHP 8.0. The modern replacement is `NumberFormatter::formatCurrency()` from the `intl` extension. Audit XOOPS core for `money_format()` calls. If none remain, remove this dependency. If calls exist, plan migration to `NumberFormatter` and then remove the polyfill.
- [ ] 4.3 **Monitor `tecnickcom/tcpdf` succession** — TCPDF is in "support-only mode" with `tecnickcom/tc-lib-pdf` as the intended successor (v8.1.0+ released). However, tc-lib-pdf does not yet have full feature parity (e.g., no FPDI/PDF-import support). Keep `^6.10` for now, but create a tracking issue to revisit when tc-lib-pdf reaches feature parity.

## 5. Smarty 4 to 5 Migration Preparation

- [ ] 5.1 **Audit Smarty 4 usage in XOOPS core** — Smarty 4.5.6 is the final 4.x release. Identify all Smarty API calls in XoopsCore25 that will break in Smarty 5: (a) class name changes (`Smarty_Internal_Template` -> `\Smarty\Template`), (b) removed `getVariable()` (use `getTemplateVars()`), (c) removed legacy tags (`{block_parent}`, `{parent}`, `{block_child}`, `{child}`), (d) removed PHP functions as modifiers.
- [ ] 5.2 **Create Smarty 5 migration guide** — Document all breaking changes relevant to XOOPS in a tracking issue or migration doc. Estimate effort (Tiki Wiki reported 500+ file changes for their migration).
- [x] 5.3 **Add Smarty 5 conflict rule** — Added `"conflict": { "smarty/smarty": ">=5.0" }` to prevent accidental Smarty 5 installation before XOOPS core is ready. Remove when items 5.1 and 5.2 are complete.
- [ ] 5.4 **When XOOPS core is ready, remove conflict and bump Smarty constraint** — Change `"smarty/smarty": "^4.5.6"` to `"smarty/smarty": "^5.0"` (or `"^4.5.6 || ^5.0"` for a transitional period). This is blocked on items 5.1 and 5.2.

## 6. Project Hygiene & Documentation

- [x] 6.1 **Fix CONTRIBUTING.md upstream reference** — Changed PR URL from `XoopsModules25x/mymenus` (copy-paste error) to `XOOPS/base-requires25`.
- [x] 6.2 **Update bug-report.yml template** — Changed "Module Version" to "XOOPS Version" with default `2.5.12`. Added PHP 8.5 to the PHP version dropdown.
- [x] 6.3 **Update feature-request.yml template** — Changed "This XOOPS Module is a work in progress!" to "This XOOPS base-requires25 metapackage is a work in progress!" and "using the module" to "using the package".
- [x] 6.4 **Add `.gitattributes` file** — Created with LF normalization, msysgit diff helpers, and export-ignore rules for non-essential files (docs/, .github/, CLAUDE.md, .scrutinizer.yml). Matches XMF/RegDom pattern.
- [ ] 6.5 **Improve README.md** — Current README is minimal. Add: (a) badge for latest Packagist version, (b) list of included dependencies with brief descriptions, (c) PHP version requirements, (d) link to XoopsCore25.
- [ ] 6.6 **Add CHANGELOG.md** — Track dependency version changes across releases. Each entry should note which package changed, from/to version, and why (security fix, PHP compat, feature).
- [x] 6.7 **Clean up `.gitignore`** — Aligned with XMF/RegDom pattern. Added `build/` and `coverage.clover` entries.
- [x] 6.8 **Add `.scrutinizer.yml`** — Created Scrutinizer CI config that runs `composer validate --strict --no-check-publish`. Adapted for metapackage (no PHP analyzer, no code coverage).
- [x] 6.9 **Create `.github/copilot-instructions.md`** — Adapted from XMF template for metapackage context. Covers Composer conventions, dependency management, PHP compatibility, and PR checklist.

## 7. CI/CD & Automation

- [ ] 7.1 **Add GitHub Actions workflow for `composer validate`** — Create `.github/workflows/validate.yml` that runs `composer validate --strict` on pushes and PRs. This catches JSON syntax errors, missing fields, and constraint issues automatically.
- [ ] 7.2 **Add GitHub Actions workflow for dependency resolution testing** — Run `composer update --dry-run --with-dependencies` against multiple PHP versions (7.4, 8.0, 8.1, 8.2, 8.3, 8.4, 8.5) to ensure all dependencies resolve on every supported version.
- [ ] 7.3 **Add Dependabot or Renovate configuration** — Automate dependency update PRs. Create `.github/dependabot.yml`:
  ```yaml
  version: 2
  updates:
    - package-ecosystem: "composer"
      directory: "/"
      schedule:
        interval: "weekly"
  ```
- [ ] 7.4 **Add security audit step** — Run `composer audit` in CI to check for known vulnerabilities in dependencies (requires Composer 2.4+).

## 8. Composer Schema Enhancements

- [x] 8.1 **Add `funding` key** — Added three funding sources matching XMF/RegDom: GitHub Sponsors, Open Collective, XOOPS donations page.
- [x] 8.2 **Add `keywords`** — Added `["xoops", "cms", "dependencies", "metapackage"]` for Packagist searchability.
- [x] 8.3 **Add `conflict` rules** — Added `"smarty/smarty": ">=5.0"` to prevent accidental Smarty 5 installation.
- [x] 8.4 **Add `suggest` section** — Added `ext-intl` (for locale-aware formatting) and `ext-imagick` (for advanced image processing) as optional recommendations.
- [ ] 8.5 **Consider adding `require-dev` section** — Even though this is a metapackage, consider adding `"roave/security-advisories": "dev-latest"` to block packages with known vulnerabilities during development. Note: metapackages cannot have `require-dev` in Composer — this may need to be documented as a limitation.

## 9. Long-Term Architecture Considerations

- [ ] 9.1 **Evaluate splitting polyfills into a separate metapackage** — The polyfill packages (`symfony/polyfill-iconv`, `symfony/polyfill-mbstring`, `boenrobot/money_format_polyfill`) serve a different purpose than the functional dependencies. Consider whether a `xoops/polyfills25` metapackage would provide clearer separation of concerns.
- [ ] 9.2 **Plan PHP 7.4 EOL cutoff** — PHP 7.4 reached EOL in Nov 2022. Decide on a timeline to drop PHP 7.4 support, which would allow using PHP 8.0+ features (named arguments, union types, match expressions, etc.) in XOOPS core. Dropping 7.4 would also simplify dependency management since most modern packages require PHP 8.0+.
- [ ] 9.3 **Coordinate version tagging with XoopsCore25** — Establish a versioning policy where base-requires25 tags (e.g., v1.2.0) correspond to XoopsCore25 release milestones, making it clear which dependency set belongs to which core version.

## 10. Cross-Repository Alignment

- [x] 10.1 **Align bug-report.yml PHP dropdown across all three repos** — All three repos (base-requires25, XMF, RegDom) now use PHP 7.4–8.5 in the dropdown. XMF and RegDom still show 7.4–8.4 and should be updated separately to add 8.5.
- [x] 10.2 **Align composer.json structure with XMF/RegDom** — Added `keywords`, `funding`, `suggest`, `conflict` sections matching the pattern used in XMF and RegDom.
- [x] 10.3 **Align .gitattributes with XMF/RegDom** — Follows same pattern: LF normalization, msysgit diff rules, export-ignore for non-essential files.
- [x] 10.4 **Align .gitignore with XMF/RegDom** — Same core entries: `*~`, `\#*`, `*.bak`, `.idea/`, `vendor/`, `composer.lock`, `build/`, `coverage.clover`.
- [ ] 10.5 **Fix CONTRIBUTING.md in XMF and RegDom** — Both repos still reference `XoopsModules25x/mymenus` for PRs. Should be updated to their respective repository URLs. (Tracked here for awareness; changes must be made in those repos.)
- [ ] 10.6 **Add PHP 8.5 to XMF and RegDom bug-report.yml** — Both repos currently list PHP 7.4–8.4 only. Add 8.5 to match base-requires25. (Tracked here for awareness; changes must be made in those repos.)
