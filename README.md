# Developer Toolbox

[![GitHub Pages](https://github.com/ttomohisa/httpapps-developer-toolbox/actions/workflows/deploy-pages.yml/badge.svg)](https://github.com/ttomohisa/httpapps-developer-toolbox/actions/workflows/deploy-pages.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Single HTML](https://img.shields.io/badge/distribution-single%20HTML-0ea5e9)](https://ttomohisa.github.io/httpapps-developer-toolbox/)

[日本語 README](README.ja.md)

**Developer Toolbox** is a local-first developer toolbox that puts small, frequently used utilities into one self-contained HTML file.

Instead of opening separate sites for Base64, UNIX timestamps, JWTs, cron, regex, JSON, hashes, and similar tasks, paste a value into **Smart Input** or open the tool you need directly. Processing stays in the browser.

![Developer Toolbox screenshot](assets/screenshot.png)

## Tools

- **Encode:** Base64 / URL / HTML Entity / Unicode / Hex / Data URI
- **Data:** JSON / YAML / CSV / JSON Diff / JSONPath
- **Text:** Case Converter / Sort Lines / Deduplicate / Character & Byte Count / Escape
- **Time:** UNIX Timestamp / ISO 8601 / Date Difference / Cron
- **Security:** JWT Decoder / Hash / HMAC / Random Generator
- **Developer:** Regex / UUID / URL Parser / HTTP Status / Number Base / CIDR
- **Web:** Color Converter / px ↔ rem / CSS Tools

A total of 33 utilities are bundled into one single HTML file with no runtime network dependency.

## Smart Input

Paste JSON, a JWT, URL, Base64 string, UNIX timestamp, or plain text at the top of the page. Developer Toolbox detects likely formats locally and suggests a matching tool. Selecting a suggestion transfers the current value to that tool without storing it.

## Navigation

- Search all tools from the desktop sidebar.
- On smartphones, use the compact **Tools** picker instead of scrolling through a long tool catalog.
- Press `Ctrl+K` / `Cmd+K` to open the command palette. Japanese and English aliases are searchable, and `↑` / `↓` + `Enter` work without leaving the keyboard.
- Direct links such as `#base64`, `#jwt`, `#cron`, and `#regex` open a tool immediately.
- Star favorite tools to also show them in the Favorites section; they remain visible in their original categories.

## Privacy

- No runtime CDN or API request
- No analytics or telemetry
- CSP uses `connect-src 'none'`
- Smart Input and utility input/output are **not** stored in localStorage
- Only language and favorite tool IDs are stored locally
- Selected files remain in the browser and are used only for local hashing

JWT decoding does **not** verify a signature. Cron results use common five-field syntax and the device local timezone. File hashing reads the whole file into browser memory.

## Build

On Windows 10/11, double-click:

```text
build-standalone.bat
```

or run the PowerShell builder directly.

The build generates:

```text
dist/
├─ index.html
├─ index.self-extract.html
├─ dependency-manifest.json
├─ self-extract-manifest.json
└─ .nojekyll
```

`dist/index.html` is the readable GitHub Pages artifact. `dist/index.self-extract.html` gzip-compresses that HTML and restores it locally with the browser's `DecompressionStream` API.

### File size

- Regular `index.html`: about 168 KiB
- Self-extracting `index.self-extract.html`: about 61 KiB

The regular Pages build intentionally avoids aggressive minification because the small extra savings are not worth the added maintenance and verification risk. Use the self-extracting build when file size matters; it keeps the full feature set and adds only a short in-browser gzip expansion step at startup.

The app currently uses no third-party runtime libraries.

## Development

Edit `src/index.template.html`, not generated files under `dist/`. Product behavior and acceptance criteria are documented in [APP_SPEC.md](APP_SPEC.md). The repository keeps the same build and verification contract as `htmlapps-template`.

## License

Copyright © 2026 ttomohisa

Released under the [MIT License](LICENSE).
