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

関連リポジトリの一覧は [repositories.md](repositories.md) を参照。
