# Developer Toolbox

[![GitHub Pages](https://github.com/ttomohisa/httpapps-developer-toolbox/actions/workflows/deploy-pages.yml/badge.svg)](https://github.com/ttomohisa/httpapps-developer-toolbox/actions/workflows/deploy-pages.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Single HTML](https://img.shields.io/badge/distribution-single%20HTML-0ea5e9)](https://ttomohisa.github.io/httpapps-developer-toolbox/)

[English README](README.md)

**Developer Toolbox** は、開発中にちょっとだけ使いたくなる小粒なユーティリティを、1つの単一HTMLへまとめたローカル処理の開発者ツールボックスです。

Base64、UNIX timestamp、JWT、cron、正規表現、JSON、Hashなどのために毎回別サイトを探す代わりに、上部の **Smart Input** へ貼り付けるか、必要なツールを直接開いて使えます。入力内容は外部へ送信しません。

![Developer Toolboxの画面](assets/screenshot.png)

## 収録ツール

- **Encode:** Base64 / URL / HTML Entity / Unicode / Hex / Data URI
- **Data:** JSON / YAML / CSV / JSON Diff / JSONPath
- **Text:** Case Converter / Sort Lines / Deduplicate / Character & Byte Count / Escape
- **Time:** UNIX Timestamp / ISO 8601 / Date Difference / Cron
- **Security:** JWT Decoder / Hash / HMAC / Random Generator
- **Developer:** Regex / UUID / URL Parser / HTTP Status / Number Base / CIDR
- **Web:** Color Converter / px ↔ rem / CSS Tools

合計33ツールを、外部通信なしの単一HTMLにまとめています。

## Smart Input

画面上部へJSON、JWT、URL、Base64、UNIX timestamp、通常の文字列などを貼り付けると、形式をブラウザー内で判定して適したツールを候補表示します。候補を選ぶと、その値を保存せずメモリ上で対象ツールへ渡します。

## 操作

- PCでは左側から全ツールを検索できます。
- スマホでは長いツール一覧を表示せず、**「ツール」** ボタンからコンパクトな選択画面を開きます。
- `Ctrl+K` / `Cmd+K` で検索パレットを開けます。日本語・英語の別名検索に対応し、`↑` / `↓` + `Enter` だけでも選択できます。
- `#base64`、`#jwt`、`#cron`、`#regex` などのURLハッシュから直接開けます。
- よく使うツールに★を付けると上部の「お気に入り」にも表示され、元のカテゴリにもそのまま残ります。
- Base64、URL、Unicode、Hexなどの軽量ツールは入力に応じてリアルタイム変換します。
- 対応ツールの結果欄から **「別ツールへ」** を選ぶと、その結果を別のツールへ直接渡せます。
- 変換系ツールでは **「入れ替え」** で入力と結果を素早く往復できます。
- 各ツールの入力値はページを開いている間だけメモリに保持されるため、別ツールへ移動して戻っても作業を続けられます。

## プライバシー

- 実行時のCDN・API通信なし
- 分析・テレメトリーなし
- CSPは `connect-src 'none'`
- Smart Inputや各ツールの入力・出力は **localStorageへ保存しません**
- 各ツールの入力値はタブを開いている間だけメモリ上に保持し、リロードすると消えます
- 保存するのは言語とお気に入りのツールIDだけです
- 選択したファイルはブラウザー内だけでHash計算に使用します

JWTはデコードのみで、署名の正当性は検証しません。Cronは一般的な5フィールド形式と端末のローカルタイムゾーンを使います。ファイルHashはファイル全体をブラウザーのメモリへ読み込みます。

## ビルド

Windows 10/11では次をダブルクリックします。

```text
build-standalone.bat
```

生成物：

```text
dist/
├─ index.html
├─ index.self-extract.html
├─ dependency-manifest.json
├─ self-extract-manifest.json
└─ .nojekyll
```

`dist/index.html` が可読なGitHub Pages向け通常版です。`dist/index.self-extract.html` は通常版をgzip圧縮し、ブラウザー標準の `DecompressionStream` で端末内展開します。

### ファイルサイズ

- 通常版 `index.html`: 約168 KiB
- 自己解凍版 `index.self-extract.html`: 約61 KiB

通常版をさらに強くミニファイすると保守性や検証コストに対して削減効果が小さいため、GitHub Pages向け通常版は可読性と安定性を優先しています。ファイルサイズを優先する場合は、機能をすべて保持した自己解凍版を利用できます。自己解凍版は起動時にブラウザー内でgzipを展開する短い処理が入ります。

現時点では第三者ランタイムライブラリを使用していません。

## 開発

生成済みの `dist` を直接編集せず、`src/index.template.html` を変更して再ビルドしてください。製品仕様と受入条件は [APP_SPEC.md](APP_SPEC.md) にまとめています。ビルドと検証の仕組みは `htmlapps-template` の契約に準拠しています。

## ライセンス

Copyright © 2026 ttomohisa

[MIT License](LICENSE) で公開しています。
