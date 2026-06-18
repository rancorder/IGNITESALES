# Security Policy — Sales Verification OS

この repo は現在 Public のため、実商談ログ・架電ログ・個人情報・顧客固有情報をそのまま置かない。

## Public repo に置いてよいもの

- テンプレート
- 抽象化した運用ルール
- サンプルデータ
- 匿名化済みの検証ログ
- 公開可能なサービス説明
- Vercel 表示用のサニタイズ済み summary

## Public repo に置いてはいけないもの

- 電話番号
- 個人メールアドレス
- 個人名が特定できる商談ログ
- 顧客の未公開予算・導入時期・決裁構造
- 商談録音文字起こしの生データ
- 顧客との未公開チャット全文
- 見積・原価・社内判断の詳細
- 顧客提示前の内部戦略

## Private repo 化した場合の推奨

実運用では `sales-verification-os` の Private repo を別途作り、このファイル群を移植する。

Private repo でも以下は削除・マスク推奨。

```text
電話番号        → [PHONE_REDACTED]
個人メール      → [EMAIL_REDACTED]
個人名          → 役職または人物ID
生ログ全文      → 必要箇所だけFACT抽出
顧客名          → project_id または client_code
```

## 公開ビューアの原則

`public/log-os/data/` には、公開しても問題ない summary のみ置く。
顧客別URLで見せる場合でも、静的サイトのため完全なアクセス制御ではない。
本当に顧客別閲覧制限が必要な場合は、Vercel Middleware / Next.js / 認証付き実装に移行する。

## Codex向け注意

Codex は GitHub repo を読めるが、公開してよい情報かどうかは自動では判断しきれない。
ファイル作成時は、必ず以下を確認する。

1. 個人情報が含まれていないか
2. 顧客固有の機密情報が含まれていないか
3. Public view に出す必要がある内容か
4. `FACT` と `ANALYSIS` が混ざっていないか
5. 外部共有用と内部検証用が混ざっていないか
