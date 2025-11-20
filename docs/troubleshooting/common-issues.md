# よくある問題と解決方法

このドキュメントでは、Kiroを使用する際によく遭遇する問題とその解決方法を説明します。問題が発生した際は、まずこちらを確認してください。

## インストール関連の問題

### 1. Kiroがインストールできない

**症状:**
- インストールコマンドが失敗する
- 権限エラーが表示される

**原因と解決方法:**

#### Node.jsのバージョンが古い
```bash
# Node.jsのバージョンを確認
node --version

# 推奨: Node.js 18以上を使用
# Node.jsを最新版にアップデート
```

#### 権限の問題（macOS/Linux）
```bash
# sudoを使用してインストール
sudo npm install -g kiro

# または、npmの権限設定を変更
npm config set prefix ~/.npm-global
export PATH=~/.npm-global/bin:$PATH
```

#### ネットワーク接続の問題
```bash
# プロキシ設定が必要な場合
npm config set proxy http://proxy.company.com:8080
npm config set https-proxy http://proxy.company.com:8080
```

### 2. Kiroコマンドが見つからない

**症状:**
```
kiro: command not found
```

**解決方法:**
```bash
# PATHの確認
echo $PATH

# npmのグローバルインストールパスを確認
npm config get prefix

# .bashrcまたは.zshrcにパスを追加
export PATH="$(npm config get prefix)/bin:$PATH"
```

## 設定関連の問題

### 3. MCP設定が反映されない

**症状:**
- MCP設定を追加したが、ツールが使用できない
- 設定ファイルを変更しても反映されない

**解決方法:**

#### 設定ファイルの場所を確認
```bash
# ワークスペース設定（プロジェクト固有）
.kiro/settings/mcp.json

# ユーザー設定（グローバル）
~/.kiro/settings/mcp.json
```

> 💡 **設定のマージ**: 両方の設定ファイルが存在する場合、設定はマージされ、ワークスペースレベルの設定が優先されます。

#### uvxのインストール確認
```bash
# uvとuvxのインストール確認
uv --version
uvx --version

# インストールされていない場合
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc  # または ~/.zshrc
```

> ⚠️ **重要**: `uvx install <package>`のようなコマンドは存在しません。`uvx`は指定されたパッケージを自動的にダウンロードして実行します。

#### JSON形式の確認
```json
{
  "mcpServers": {
    "aws-docs": {
      "command": "uvx",
      "args": ["awslabs.aws-documentation-mcp-server@latest"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      },
      "disabled": false,
      "autoApprove": [
        "read_documentation",
        "search_documentation"
      ]
    }
  }
}
```

#### MCPサーバーの再接続
1. 設定ファイルを保存（自動的に再接続される）
2. または、MCP Server viewで該当サーバーを確認
3. コマンドパレットから「MCP」を検索して再接続

#### MCPサーバーのテスト
> 💡 **推奨方法**: 設定確認前に、直接ツールを試すのが推奨されます。

```
# Kiroのチャットで直接テスト
Amazon S3について教えてください。

# MCPが正常に動作していれば、
# AWS Documentation MCPを使用して情報を取得します
```

### 4. Steeringファイルが適用されない

**症状:**
- Steeringファイルを作成したが、AIの動作が変わらない
- 設定が無視されているように見える

**解決方法:**

#### ファイルの配置場所を確認
```
.kiro/steering/
├── 00-project-basics.md      # 常に適用
├── 10-coding-standards.md    # 常に適用
├── 30-frontend-rules.md      # 条件付き適用
└── 90-deployment.md          # 手動適用
```

#### Front-matter設定の確認

**常に適用:**
```markdown
---
inclusion: always
---

# プロジェクト基本情報
```

**条件付き適用:**
```markdown
---
inclusion: fileMatch
fileMatchPattern: 'src/**/*.tsx'
---

# React コンポーネント規約
```

> ⚠️ **注意**: `fileMatchPattern`には必ずクォート（`'`または`"`）が必要です。

**手動適用:**
```markdown
---
inclusion: manual
---

# デプロイメント手順書

使用方法: #Steering deployment-procedures
```

#### ファイル参照の確認

外部ファイルを参照する場合：

```markdown
---
inclusion: always
---

# API設計ガイド

## OpenAPI仕様
#[[file:../docs/openapi.yaml]]
```

**確認事項:**
- 相対パスが正しいか
- 参照ファイルが存在するか
- ファイルパスにスペースが含まれていないか

## 使用時の問題

### 5. AIの応答が期待と異なる

**症状:**
- AIが意図しない動作をする
- 生成されるコードが要求と合わない

**解決方法:**

#### コンテキストの確認
```bash
# 現在のコンテキストを確認
#File, #Folder, #Problems, #Terminal, #Git Diff, #Codebase
```

#### プロンプトの改善
- より具体的な指示を与える
- 期待する結果の例を示す
- ステップバイステップで指示する

#### Steeringファイルの活用
```markdown
# プロジェクト固有のルール
- コーディング規約
- 使用するライブラリ
- 避けるべきパターン
```

### 6. ファイル操作でエラーが発生する

**症状:**
```
Permission denied
File not found
Cannot write to file
```

**解決方法:**

#### ファイル権限の確認
```bash
# ファイル権限を確認
ls -la filename

# 権限を変更
chmod 644 filename
```

#### ディスク容量の確認
```bash
# ディスク使用量を確認
df -h

# 不要なファイルを削除
```

#### ファイルロックの解除
- 他のエディタでファイルが開かれていないか確認
- プロセスが異常終了していないか確認

### 7. パフォーマンスの問題

**症状:**
- Kiroの動作が遅い
- 応答に時間がかかる

**解決方法:**

#### メモリ使用量の確認
```bash
# メモリ使用量を確認
top
htop  # より詳細な情報
```

#### 大きなファイルの除外
```gitignore
# .gitignoreに追加
node_modules/
*.log
dist/
build/
```

#### コンテキストサイズの調整
- 不要なファイルをコンテキストから除外
- 大きなファイルは部分的に読み込み

## エラーメッセージ別対処法

### "Connection refused"
**原因:** ネットワーク接続の問題
**解決方法:**
1. インターネット接続を確認
2. ファイアウォール設定を確認
3. プロキシ設定を確認

### "Authentication failed"
**原因:** 認証情報の問題
**解決方法:**
1. APIキーの確認
2. 認証情報の再設定
3. アカウント状態の確認

### "Rate limit exceeded"
**原因:** API使用制限に達した
**解決方法:**
1. しばらく待ってから再試行
2. 使用頻度を調整
3. プランのアップグレードを検討

### "Invalid JSON format"
**原因:** 設定ファイルのJSON形式が不正
**解決方法:**
1. JSON形式を確認
2. オンラインJSONバリデーターを使用
3. 設定ファイルを再作成

## トラブルシューティングの手順

### 1. 基本的な確認事項
1. Kiroのバージョンを確認
2. 設定ファイルの内容を確認
3. エラーメッセージを記録
4. 再現手順を整理

### 2. ログの確認
```bash
# Kiroのログを確認
kiro --verbose

# システムログを確認（macOS）
log show --predicate 'process == "kiro"' --last 1h

# システムログを確認（Linux）
journalctl -u kiro --since "1 hour ago"
```

### 3. 設定のリセット
```bash
# 設定をバックアップ
cp -r .kiro .kiro.backup

# 設定をリセット
rm -rf .kiro
kiro init
```

### 4. 再インストール
```bash
# Kiroをアンインストール
npm uninstall -g kiro

# キャッシュをクリア
npm cache clean --force

# 再インストール
npm install -g kiro@latest
```

## サポートを求める前に

問題が解決しない場合は、以下の情報を準備してからサポートに連絡してください：

### 必要な情報
1. **環境情報**
   - OS（macOS、Windows、Linux）
   - Node.jsのバージョン
   - Kiroのバージョン

2. **エラー情報**
   - 正確なエラーメッセージ
   - エラーが発生する手順
   - 期待していた動作

3. **設定情報**
   - 関連する設定ファイルの内容
   - 使用しているMCPサーバー
   - Steeringファイルの設定

### 情報収集コマンド
```bash
# システム情報を収集
echo "OS: $(uname -a)"
echo "Node.js: $(node --version)"
echo "npm: $(npm --version)"
echo "Kiro: $(kiro --version)"

# 設定情報を確認
cat .kiro/settings/mcp.json
ls -la .kiro/steering/
```

## 関連リンク

- [Kiro公式ドキュメント](https://kiro.dev)
- [GitHub Issues](https://github.com/kiro/kiro/issues)
- [コミュニティフォーラム](https://community.kiro.dev)
- [FAQ](./faq.md)

---

**注意:** このドキュメントは定期的に更新されます。最新の情報については公式ドキュメントを確認してください。---


---

<div align="center">

| [← 🧠 コンテキスト・メモリ管理](../chapter3/context-memory-management.md) | [🏠 目次](../../README.md) | [❓ FAQ →](faq.md) |
|:---:|:---:|:---:|

</div>

---

### 🔗 関連リソース
- [❓ FAQ](faq.md)
- [📁 サンプルプロジェクト](../../examples/)
- [📖 目次](../../README.md)


## 最新機能関連の問題

### 8. Autopilot/Supervisedモードの切り替えができない

**症状:**
- モードの切り替え方法が分からない
- 意図しないモードで動作している

**解決方法:**

#### モードの確認
1. Kiroの設定画面を開く
2. Autonomy Mode設定を確認
3. 現在のモードを確認

#### モードの使い分け
- **Autopilot**: 高速開発、プロトタイピング、定型作業
- **Supervised**: 学習段階、重要な変更、本番コード

> 📖 **詳細**: [Autonomy Modes完全ガイド](../features/autonomy-modes.md)

### 9. Chat Contextが機能しない

**症状:**
- `#File`や`#Folder`が認識されない
- コンテキストが正しく読み込まれない

**解決方法:**

#### 構文の確認
```
# 正しい使用方法
#File src/components/Button.tsx
#Folder src/components/
#Problems
#Terminal
#Git Diff
#Codebase
```

#### ファイルパスの確認
- ファイルが存在するか確認
- パスが正しいか確認（相対パスまたは絶対パス）
- スペースや特殊文字が含まれていないか確認

#### コンテキストサイズの制限
- 大きすぎるファイルは分割して参照
- 必要な部分のみを指定

> 📖 **詳細**: [Chat Context完全ガイド](../features/chat-context.md)

### 10. Specsワークフローで次の段階に進めない

**症状:**
- 要件を承認したのに設計に進まない
- 明示的な承認が認識されない

**解決方法:**

#### 明示的な承認表現を使用

**OK（承認される）:**
```
「承認します」
「はい、承認します」
「良いです。次に進んでください」
「OK、設計フェーズに進んでください」
```

**NG（承認されない）:**
```
「いいと思います」
「概ね問題ないです」
「進めてください」（曖昧）
```

#### 各段階での確認
1. **要件段階**: 要件を確認 → 明示的に承認 → 設計へ
2. **設計段階**: 設計を確認 → 明示的に承認 → タスクへ
3. **タスク段階**: タスクを確認 → 明示的に承認 → 実装開始

> 📖 **詳細**: [Specsワークフロー完全ガイド](../features/specs-workflow.md)

### 11. Hooksが実行されない

**症状:**
- ファイル保存時にHookが実行されない
- 手動トリガーが動作しない

**解決方法:**

#### Hook設定の確認
```yaml
# enabled が true になっているか確認
enabled: true

# filePattern が正しいか確認
filePattern: 'src/**/*.ts'  # クォートが必要

# trigger が適切か確認
trigger: "onSave"  # または "manual"
```

#### Hook UIの確認
1. エクスプローラービューの「Agent Hooks」セクションを開く
2. Hookの状態を確認
3. 必要に応じて再有効化

#### デバッグ方法
```yaml
# 全てのファイルで試す
filePattern: "**/*"

# プロンプトを簡単にする
prompt: "Hook が実行されました！"
```

> 📖 **詳細**: [Hooks完全ガイド](../features/hooks-guide.md)
