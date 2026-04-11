# IGNITE SALES — LP

BtoB営業支援サービスのランディングページ。

## ファイル構成

```
ignite-sales/
├── public/
│   └── index.html   # LP本体
├── vercel.json       # Vercelデプロイ設定
├── .gitignore
└── README.md
```

## デプロイ手順

### 1. GitHubにプッシュ

```bash
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/<あなたのユーザー名>/ignite-sales.git
git push -u origin main
```

### 2. Vercelと連携

1. [vercel.com](https://vercel.com) にログイン
2. **Add New → Project** をクリック
3. GitHubリポジトリ `ignite-sales` をインポート
4. **Framework Preset: Other** のまま変更不要
5. **Deploy** をクリック

→ 自動でビルド＆デプロイされます。

### 3. 独自ドメイン設定（任意）

Vercel Dashboard → Project → Settings → Domains から追加できます。
