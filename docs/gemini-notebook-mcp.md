# Gemini Notebook MCP 連携・運用手順

ローカル環境（Antigravity）から公式 MCP サーバー経由で Gemini Notebook（NotebookLM）を参照・操作するための構成および保守ルールを定める。

## 1. 基本構成・ファイル配置
- **MCP サーバー名**: `gemini-notebook`
- **エンドポイント**: `https://notebook.googleapis.com/mcp`
- **GCP プロジェクト ID**: `<YOUR_GCP_PROJECT_ID>`
- **MCP 設定ファイル**: `%USERPROFILE%\.gemini\config\mcp_config.json`
- **トークン更新スクリプト**: `%USERPROFILE%\.gemini\config\update_notebook_token.ps1`
- **ワンクリック実行ファイル**: `%USERPROFILE%\Desktop\Notebookトークン更新.bat`

## 2. 利用可能な MCP ツール仕様（全7種）
Antigravity からは以下の7種類のツールを呼び出すことができる（ソース削除・ノートブック削除機能は非搭載）。

| 区分 | ツール名 | 用途・概要 |
|---|---|---|
| **読み取り系** | `list_notebooks` | アクセス可能なノートブック一覧とリソース ID の取得 |
| **読み取り系** | `get_notebook` | 指定したノートブックのメタデータ取得 |
| **読み取り系** | `list_sources` | 指定ノートブック内の登録ソース一覧と状態（`ACTIVE` 等）の取得 |
| **読み取り系** | `get_source` | 指定ソースの本文コンテンツの取得 |
| **作成・更新系** | `create_notebook` | 新規ノートブックの作成 |
| **作成・更新系** | `create_source` | 指定ノートブックへの Markdown テキスト等のソース新規追加 |
| **作成・更新系** | `update_notebook` | ノートブック表示名等の更新 |

## 3. 認証トークンの更新手順（有効期限：1時間）
OAuth 2.0 アクセストークンは発行から **1時間** で自動失効する。認証エラー（401 Unauthorized）が発生した場合、または作業開始前に以下の手順でトークンを更新する。

1. デスクトップの **`Notebookトークン更新.bat`** をダブルクリックして実行する。
2. ターミナル画面に緑色で「`更新完了: %USERPROFILE%\.gemini\config\mcp_config.json`」と表示されたら、任意のキーを押して画面を閉じる。
3. **Antigravity を一度閉じて再起動** し、新しいトークンを読み込ませる。

※「トークンの取得に失敗しました」と赤字で表示された場合は、ADC ログイン自体の期限切れであるため、PowerShell で `gcloud auth application-default login` を実行してブラウザ認証を行ったあと、再度 `Notebookトークン更新.bat` を実行する。

## 4. 安全運用・データ保護ルール
- **正本ノートブックの保護**: 既存の主要ノートブック（`CMA Theory Definition and Research Architecture Framework v2.0`、`赤十字` 等）は原則として **読み取り専用（`list_sources` / `get_source`）** として扱い、エージェントによる無断追加・改変を禁止する。
- **操作対象の明示**: ソースを追加（`create_source`）する際は、必ず対象ノートブックの正式なリソース ID（`notebooks/...`）を明示して指示する。
- **検証環境の分離**: 新しい連携テストや Markdown 同期の動作確認は、検証用ノートブック（`API接続テスト` / `notebooks/<TEST_NOTEBOOK_ID>`）で実施する。不要になったテスト用ノートブックの削除はブラウザ版 UI から手動で行う。
