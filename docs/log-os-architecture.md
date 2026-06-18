# Sales Verification OS Architecture

## 概要

Sales Verification OS は、各案件の営業活動を GitHub に蓄積し、Codex が取り出せる形にするためのファイルシステムである。

目的は「ログ保管」ではなく、AI が次回の商談設計・架電改善・資料修正・定例報告を作るための判断材料を残すこと。

## 基本フロー

```text
ChatGPTで分析・仮説作成
↓
GitHubに検証ログとして保存
↓
CodexがAGENTS.mdと案件ログを読む
↓
次回商談・資料・台本・報告に反映
↓
実結果との差分を再びログ化
```

## URL / データ分離方針

案件ごとに repo を分けない。1 repo 内で次のように分離する。

```text
projects/<project_id>/              # Codex向け内部ログ
public/log-os/data/logs/*.json      # 公開ビューア用のサニタイズ済みデータ
public/log-os/?project=<project_id> # 表示上の案件分離
```

Public repo の場合、`projects/` に実顧客の生ログを置かない。Private repo 化した場合のみ実ログを保存する。

## 推奨 project_id

project_id は小文字・英数字・ハイフンのみ。

例：

- `ageru-care`
- `raura-cba`
- `sankou`
- `t2-lab`
- `hiroshima-plastic`
- `manufacturing-dx`

## ログ1件の単位

1商談、1架電分析、1資料検証、1定例報告を1ファイルにする。

ファイル名：

```text
YYYY-MM-DD_<client-or-topic>_<type>.md
```

例：

```text
2026-06-18_dadway_2nd-meeting-verification.md
2026-06-18_call-kpi_reception-refusal-analysis.md
```

## ログ種別

- `meeting-verification`: 商談仮説検証
- `call-kpi-analysis`: 架電KPI分析
- `sales-feedback`: 商談者FB
- `customer-report`: 顧客提示用レポート
- `script-branch`: 台本・分岐図
- `weekly-report`: 定例報告

## Codex の取り出し方

Codex には以下のように依頼する。

```text
このrepoのAGENTS.mdに従って、projects/ageru-care の直近ログを読み、
定例報告の「定性的な報告 / 乖離 / 原因 / 改善 / 対策」を作成して。
FACT / ANALYSIS / NEXT / JUDGMENT は混ぜないこと。
```

## 静的ビューア

`public/log-os/` は Vercel で見るための軽量ビューア。

- `data/projects.json`: 表示する案件一覧
- `data/logs/*.json`: サニタイズ済みログ
- `app.js`: 検索・フィルタ・表示
- `styles.css`: UI

ここには公開しても問題ない内容だけを置く。
