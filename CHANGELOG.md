# base-requires25 ChangeLog

All notable changes to this project will be documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.1.10-beta2] - 2026-02-08

### Fixed
* Fix PHP constraint from `^7.4.0 || ^8.4.0` to `^7.4 || ^8.0` — previous constraint excluded PHP 8.0-8.3
* Replace global `minimum-stability: beta` with inline `@beta` flags on `xoops/xmf` and `xoops/regdom`
* Normalize version constraints to `^major.minor` style (e.g., `^1.0` instead of `^1.0.2`)

### Changed
* Change package type from `project` to `metapackage`
* Bump `xoops/regdom` from `^2.0.2-beta1` to `^2.0.2-beta3@beta`
* Bump `xoops/xmf` from `^1.2.33-beta1` to `^1.2.33-beta2@beta`

### Added
* Add `conflict` rule blocking `smarty/smarty >=5.0` until XOOPS core migrates
* Add `suggest` section for `ext-intl` and `ext-imagick`
* Add `authors`, `keywords`, `funding`, `support`, and `config` sections to `composer.json`
* Add GitHub Actions CI workflow — PHP 7.4-8.5 matrix with `composer validate --strict`
* Add Dependabot configuration for Composer and GitHub Actions
* Add Renovate configuration
* Add GitHub Copilot custom instructions (`.github/copilot-instructions.md`)
* Add `.github/CONTRIBUTING.md` with contribution guidelines
* Add `.github/ISSUE_TEMPLATE/bug-report.yml` with PHP 7.4-8.5 dropdown
* Add `.github/ISSUE_TEMPLATE/feature-request.yml` (metapackage wording)
* Add `.scrutinizer.yml` — `composer validate` only (no PHP analyzer for metapackage)
* Add `.gitattributes` with LF normalization and export-ignore rules
* Add `.gitignore` with vendor/, .idea/, build/, coverage.clover, composer.lock, callmap.json
* Add `CLAUDE.md` project guide
* Add `README.md` updates
* Pin GitHub Actions to full SHA hashes in CI workflow

## [1.1.10-beta1] - 2025-09-10

### Added
* Add `tecnickcom/tcpdf` `^6.10` for PDF generation

### Changed
* Change PHP constraint from `>=7.4.0` to `^7.4.0 || ^8.4.0`
* Bump `xoops/regdom` from `^2.0.1` to `^2.0.2-beta1`
* Bump `xoops/xmf` from `^1.2.32` to `^1.2.33-beta1`
* Bump `phpmailer/phpmailer` from `^6.9` to `^6.10`
* Bump `smarty/smarty` from `^4.5.5` to `^4.5.6`
* Bump `symfony/polyfill-iconv` from `^1.31.0` to `^1.33.0`
* Bump `symfony/polyfill-mbstring` from `^1.31.0` to `^1.33.0`
* Enable `sort-packages: true` — packages now alphabetically ordered

## [1.1.9] - 2025-03-10

### Changed
* Bump `xoops/xmf` from `^1.2.31` to `^1.2.32`

## [1.1.8] - 2025-01-05

### Added
* Add `ezyang/htmlpurifier` `^4.18` for HTML sanitization
* Add `phpmailer/phpmailer` `^6.9` for email sending
* Add `.gitattributes`

## [1.1.7] - 2024-11-27

### Changed
* Bump `xoops/regdom` from `^2.0.0` to `^2.0.1`
* Bump `xoops/xmf` from `^1.2.30` to `^1.2.31`
* Bump `smarty/smarty` from `^4.5.3` to `^4.5.5`
* Bump `symfony/polyfill-iconv` from `^1.30.0` to `^1.31.0`
* Bump `symfony/polyfill-mbstring` from `^1.30.0` to `^1.31.0`

### Added
* Add GitHub Issues templates

## [1.1.6] - 2024-07-27

### Changed
* Bump `xoops/regdom` from `^2.0.0-Alpha` to `^2.0.0` (stable release)
* Bump `symfony/polyfill-iconv` from `^1.29.0` to `^1.30.0`
* Bump `symfony/polyfill-mbstring` from `^1.29.0` to `^1.30.0`

## [1.1.5] - 2024-07-17

### Changed
* Move `xoops/regdom` from `require-dev` to `require` (now a runtime dependency)
* Remove `require-dev` section

## [1.1.4] - 2024-07-17

### Changed
* Replace `geekwright/regdom` with `xoops/regdom` `^2.0.0-Alpha` — migrate to XOOPS-namespaced package
* Move `xoops/regdom` to `require-dev` initially (promoted to `require` in v1.1.5)

### Removed
* Remove `geekwright/regdom` from `require`

## [1.1.3] - 2024-06-07

### Changed
* Raise PHP requirement from `>=5.6.0` to `>=7.4.0`
* Upgrade `smarty/smarty` from `^3.1.47` to `^4.5.3` (Smarty 4)
* Bump `xoops/xmf` from `^1.2.29` to `^1.2.30`
* Bump `geekwright/regdom` from `^1.0.0` to `^1.0.9`
* Bump `symfony/polyfill-iconv` from `^1.10.0` to `^1.29.0`
* Bump `symfony/polyfill-mbstring` from `^1.10.0` to `^1.29.0`

### Removed
* Remove `ircmaxell/password-compat` — native `password_hash()` available since PHP 5.5

## [1.1.2] - 2023-12-04

### Changed
* Bump `xoops/xmf` from `^1.2.28` to `^1.2.29`

## [1.1.1] - 2023-10-31

### Changed
* Raise PHP requirement from `>=5.3.9` to `>=5.6.0`
* Bump `xoops/xmf` from `^1.2.26` to `^1.2.28`

## [1.1.0] - 2022-10-07

### Added
* Add `smarty/smarty` `^3.1.47` — Smarty template engine now managed via Composer

## [1.0.4] - 2022-04-16

### Added
* Add `boenrobot/money_format_polyfill` `^1.0.2` — polyfill for `money_format()` removed in PHP 8.0

### Changed
* Bump `xoops/xmf` from `^1.2.25` to `^1.2.26`

## [1.0.3] - 2021-05-07

### Changed
* Bump `xoops/xmf` from `^1.2.24` to `^1.2.25`

## [1.0.2] - 2021-03-25

### Changed
* Bump `xoops/xmf` from `^1.2.21` to `^1.2.24`

## [1.0.1] - 2021-02-13

### Changed
* Bump `xoops/xmf` from `^1.2.16` to `^1.2.21`
* Change `smottt/wideimage` from exact version `1.1.2` to caret range `^1.1.4`

## [1.0.0] - 2018-11-30

### Added
* Add `symfony/polyfill-iconv` `^1.10.0` — iconv polyfill for portability

### Changed
* Bump `xoops/xmf` from `^1.2.0` to `^1.2.16`
* Bump `symfony/polyfill-mbstring` from `^1.3.0` to `^1.10.0`

## [0.2.1] - 2018-02-22

### Changed
* Fix license identifier to SPDX format (`GPL-2.0+` to `GPL-2.0-or-later`)

## [0.2.0] - 2017-02-07

### Added
* Add `geekwright/regdom` `^1.0.0` — domain registration utilities
* Add `symfony/polyfill-mbstring` `^1.3.0` — mbstring polyfill for portability

## [0.1.0] - 2017-01-22

### Added
* Initial release
* Require PHP `>=5.3.9`
* Require `xoops/xmf` `^1.2.0` — XOOPS Module Framework
* Require `ircmaxell/password-compat` `^1.0.4` — password_hash polyfill for PHP < 5.5
* Require `smottt/wideimage` `1.1.2` — image processing library (GD)

[1.1.10-beta2]: https://github.com/XOOPS/base-requires25/compare/v1.1.10-beta1...HEAD
[1.1.10-beta1]: https://github.com/XOOPS/base-requires25/compare/v1.1.9...v1.1.10-beta1
[1.1.9]: https://github.com/XOOPS/base-requires25/compare/v1.1.8...v1.1.9
[1.1.8]: https://github.com/XOOPS/base-requires25/compare/v1.1.7...v1.1.8
[1.1.7]: https://github.com/XOOPS/base-requires25/compare/v1.1.6...v1.1.7
[1.1.6]: https://github.com/XOOPS/base-requires25/compare/v1.1.5...v1.1.6
[1.1.5]: https://github.com/XOOPS/base-requires25/compare/v1.1.4...v1.1.5
[1.1.4]: https://github.com/XOOPS/base-requires25/compare/v1.1.3...v1.1.4
[1.1.3]: https://github.com/XOOPS/base-requires25/compare/v1.1.2...v1.1.3
[1.1.2]: https://github.com/XOOPS/base-requires25/compare/v1.1.1...v1.1.2
[1.1.1]: https://github.com/XOOPS/base-requires25/compare/v1.1.0...v1.1.1
[1.1.0]: https://github.com/XOOPS/base-requires25/compare/v1.0.4...v1.1.0
[1.0.4]: https://github.com/XOOPS/base-requires25/compare/v1.0.3...v1.0.4
[1.0.3]: https://github.com/XOOPS/base-requires25/compare/v1.0.2...v1.0.3
[1.0.2]: https://github.com/XOOPS/base-requires25/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/XOOPS/base-requires25/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/XOOPS/base-requires25/compare/v0.2.1...v1.0.0
[0.2.1]: https://github.com/XOOPS/base-requires25/compare/v0.2.0...v0.2.1
[0.2.0]: https://github.com/XOOPS/base-requires25/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/XOOPS/base-requires25/releases/tag/v0.1.0
