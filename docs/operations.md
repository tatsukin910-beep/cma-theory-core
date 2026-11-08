# 運用ルールと関連リポジトリ

## 運用ルール Version 2.2（要点）

### 役割分担

| ツール | 役割 |
| --- | --- |
| X / Grok | 観測 |
| Gemini | 構造化 |
| GitHub | 履歴 |
| Antigravity | 実装 |
| gcloud | デプロイ |
| X Subscriptions | 還元 |

### ワークフロー

観測 → 構造化 → Issue化 → 実装 → 差分確認・コミット・デプロイ → 還元

### 原則

- 変更は必ず diff 確認後にコミットする。
- 正本は Zenodo の Theory Definition v2.0（DOI: [10.5281/zenodo.21876469](https://doi.org/10.5281/zenodo.21876469)）。

## 関連リポジトリ一覧

| リポジトリ | 位置づけ |
| --- | --- |
| cma-theory-core | 正本履歴ハブ（現行・中心） |
| cma-os-v2 | 証拠記録PWA（現行寄り） |
| cma-cognitive-field | 5層可視化（現行寄り） |
| tatsuki-nakamura | 研究サイト下書き（ドメイン未接続） |
| cma-perception-field-react / cma-perception-field / cma-matrix-cylinder | 可視化プロトタイプ群（旧版寄り） |
| cognitive-os4.0- / cma-visualizer- / cma-os | OS・可視化系の旧版・プロトタイプ |
| live-timestamp-terminal | ユーティリティPWA（研究外） |
