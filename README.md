# IGNITE SALES — LP / Sales Verification OS

BtoB営業支援LPに、Sales Verification OS の土台を追加したリポジトリです。

## Added

- `AGENTS.md`: Codex rules
- `docs/`: architecture and retrieval guide
- `templates/`: markdown templates
- `schemas/`: JSON schema
- `site/`: Vercel static viewer

## Vercel

`vercel.json` uses:

```json
{
  "outputDirectory": "site"
}
```

## Codex prompt

```text
Read AGENTS.md and the target project logs. Separate FACT, ANALYSIS, NEXT, and JUDGMENT.
```

## Security

This repository is public. Keep real customer notes in a private repository.
