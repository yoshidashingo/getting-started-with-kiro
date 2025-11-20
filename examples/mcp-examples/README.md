# MCP設定例集

このディレクトリには、様々なMCPサーバーの設定例が含まれています。

## 利用可能な設定例

### 1. AWS Documentation MCP
- **ファイル**: `aws-documentation-mcp.json`
- **用途**: AWSサービスのドキュメント参照
- **必要な準備**: `uv`のインストール

### 2. Playwright MCP
- **ファイル**: `playwright-mcp.json`
- **用途**: ブラウザ自動テスト
- **必要な準備**: `uv`のインストール

### 3. GitHub MCP
- **ファイル**: `github-mcp.json`
- **用途**: GitHubリポジトリ操作
- **必要な準備**: GitHubトークン

### 4. 複数MCP統合設定
- **ファイル**: `multiple-mcp-servers.json`
- **用途**: 複数のMCPサーバーを同時使用

## 使用方法

### 1. 設定ファイルのコピー

```bash
# ワークスペース設定にコピー
cp examples/mcp-examples/aws-documentation-mcp.json .kiro/settings/mcp.json

# または、ユーザー設定にコピー
cp examples/mcp-examples/aws-documentation-mcp.json ~/.kiro/settings/mcp.json
```

### 2. 必要に応じて編集

```bash
# エディタで開いて編集
code .kiro/settings/mcp.json
```

### 3. Kiroで確認

設定ファイルを保存すると、Kiroが自動的に設定を読み込みます。

## 前提条件

### uvのインストール

ほとんどのMCPサーバーは`uvx`コマンドを使用します：

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Homebrew
brew install uv

# pip
pip install uv

# インストール確認
uv --version
uvx --version
```

### 環境変数の設定

一部のMCPサーバーは環境変数が必要です：

```bash
# GitHub MCP用
export GITHUB_TOKEN="your_github_token"

# カスタムMCP用
export API_KEY="your_api_key"
```

## トラブルシューティング

### MCPサーバーが起動しない

```bash
# 1. uvのインストール確認
uv --version

# 2. MCPサーバーの手動実行テスト
uvx awslabs.aws-documentation-mcp-server@latest

# 3. 設定ファイルの構文確認
python -m json.tool .kiro/settings/mcp.json
```

### ツールが認識されない

1. MCP Server Viewで接続状態を確認
2. `autoApprove`リストを確認
3. `disabled`が`false`になっているか確認

## 詳細情報

各MCPサーバーの詳細な使用方法については、以下を参照してください：

- [MCP設定完全ガイド](../../docs/features/mcp-configuration.md)
- [AWS MCP設定](../../docs/chapter2/aws-mcp-setup.md)
- [Playwright MCPテスト](../../docs/chapter1/playwright-mcp-testing.md)
