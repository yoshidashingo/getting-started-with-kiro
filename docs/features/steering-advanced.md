# Steering高度な使用方法ガイド

## 概要

Steeringファイルは、Kiroの動作をカスタマイズし、プロジェクト固有の知識をAIに伝えるための強力な機能です。このガイドでは、Steeringファイルの高度な使用方法、ベストプラクティス、実践的なテクニックについて詳しく解説します。

## Steeringファイルの基本構造

### 配置場所

```
.kiro/steering/
├── always-included.md       # 常に適用
├── conditional-*.md          # 条件付き適用
└── manual-*.md              # 手動呼び出し
```

### Front-matter設定

```markdown
---
inclusion: always
---

# ドキュメント内容
```

## Front-matter詳細仕様

### inclusion: always（常に適用）

```markdown
---
inclusion: always
---

# プロジェクト基本情報

このファイルは全てのKiro操作で自動的に読み込まれます。

## プロジェクト概要
- 名前: タスク管理アプリ
- 技術スタック: React + Node.js + PostgreSQL
- 開発期間: 2024年1月〜3月
```

**使用シーン:**
- プロジェクトの基本情報
- コーディング規約
- セキュリティガイドライン
- 共通の設計原則

### inclusion: fileMatch（条件付き適用）

```markdown
---
inclusion: fileMatch
fileMatchPattern: 'src/components/**/*.tsx'
---

# React コンポーネント開発ガイドライン

このファイルは、src/components/配下の.tsxファイルを
編集する時のみ適用されます。

## コンポーネント設計原則
- 単一責任の原則を遵守
- Props の型定義を必須とする
- デフォルトプロパティを適切に設定
```

**fileMatchPattern の書き方:**

```yaml
# 特定のディレクトリ
fileMatchPattern: 'src/components/**/*.tsx'

# 特定のファイル名パターン
fileMatchPattern: '*.test.ts'

# 複数の拡張子
fileMatchPattern: 'src/**/*.{ts,tsx}'

# ルートディレクトリの特定ファイル
fileMatchPattern: 'package.json'
```

**使用シーン:**
- フロントエンド固有のルール
- バックエンド固有のルール
- テストファイル固有のガイドライン
- 設定ファイル固有の注意事項

### inclusion: manual（手動呼び出し）

```markdown
---
inclusion: manual
---

# デプロイメント手順書

このファイルは、チャットで明示的に参照した時のみ読み込まれます。

使用方法: #Steering deployment-procedures

## 本番デプロイ手順
1. テストの実行確認
2. ビルドの作成
3. ステージング環境での検証
4. 本番環境へのデプロイ
5. ヘルスチェック
```

**使用シーン:**
- デプロイメント手順
- トラブルシューティングガイド
- 特殊な操作手順
- 緊急時の対応マニュアル

## ファイル参照機能

### 基本的な使い方

```markdown
---
inclusion: always
---

# API設計ガイド

## OpenAPI仕様
最新のAPI仕様は以下を参照：

#[[file:../docs/openapi.yaml]]

この仕様に従ってAPIを実装してください。
```

### 相対パスの指定

```markdown
# Steeringファイルからの相対パス
#[[file:../docs/api-spec.yaml]]          # 1つ上のdocsフォルダ
#[[file:../../config/database.yml]]      # 2つ上のconfigフォルダ
#[[file:./templates/component.tsx]]      # 同じフォルダのtemplatesサブフォルダ
```

### 複数ファイルの参照

```markdown
---
inclusion: always
---

# プロジェクト設計ドキュメント

## アーキテクチャ
#[[file:../docs/architecture.md]]

## データベース設計
#[[file:../docs/database-schema.sql]]

## API仕様
#[[file:../docs/openapi.yaml]]

## デプロイメント設定
#[[file:../docker-compose.yml]]
```

### 活用シーン

#### 1. OpenAPI仕様の活用

```markdown
---
inclusion: fileMatch
fileMatchPattern: 'src/api/**/*.ts'
---

# API実装ガイド

## API仕様
#[[file:../docs/openapi.yaml]]

上記の仕様に厳密に従って実装してください。

## 実装ルール
- エンドポイントパスは仕様と完全一致
- レスポンス形式は仕様通り
- エラーコードは仕様で定義されたもののみ使用
```

#### 2. GraphQLスキーマの活用

```markdown
---
inclusion: fileMatch
fileMatchPattern: 'src/graphql/**/*.ts'
---

# GraphQL実装ガイド

## スキーマ定義
#[[file:../schema/schema.graphql]]

## 実装ガイドライン
- リゾルバーはスキーマと完全一致
- 型定義はスキーマから自動生成
- N+1問題に注意（DataLoaderを使用）
```

#### 3. 設定ファイルの参照

```markdown
---
inclusion: always
---

# 環境設定ガイド

## 開発環境設定
#[[file:../.env.example]]

## Docker設定
#[[file:../docker-compose.yml]]

## CI/CD設定
#[[file:../.github/workflows/ci.yml]]

これらの設定ファイルを参考に、
環境に応じた適切な設定を行ってください。
```

## 高度な活用パターン

### パターン1: 階層的なSteering構造

```
.kiro/steering/
├── 00-project-basics.md          # 最優先（常に適用）
├── 10-coding-standards.md        # コーディング規約
├── 20-security-guidelines.md     # セキュリティ
├── 30-frontend-rules.md          # フロントエンド（条件付き）
├── 31-backend-rules.md           # バックエンド（条件付き）
├── 40-testing-guidelines.md      # テスト
└── 90-deployment-procedures.md   # デプロイ（手動）
```

**命名規則:**
- 数字プレフィックスで優先順位を示す
- 00-09: 最優先（プロジェクト基本情報）
- 10-29: 一般的なルール
- 30-39: 技術スタック固有
- 40-89: 特定の用途
- 90-99: 手動呼び出し用

### パターン2: 環境別Steering

```markdown
---
inclusion: always
---

# 環境別設定ガイド

## 現在の環境
環境変数 NODE_ENV を確認してください。

## 開発環境 (development)
#[[file:../config/development.yml]]

- デバッグログを有効化
- ホットリロードを使用
- モックAPIを利用可能

## ステージング環境 (staging)
#[[file:../config/staging.yml]]

- 本番に近い設定
- パフォーマンス監視を有効化
- E2Eテストを実行

## 本番環境 (production)
#[[file:../config/production.yml]]

- エラーログのみ出力
- セキュリティヘッダーを強化
- 監視とアラートを設定
```

### パターン3: 役割別Steering

```
.kiro/steering/
├── role-frontend-developer.md
├── role-backend-developer.md
├── role-devops-engineer.md
└── role-qa-engineer.md
```

```markdown
---
inclusion: manual
---

# フロントエンド開発者向けガイド

使用方法: #Steering role-frontend-developer

## 担当範囲
- React コンポーネントの実装
- UIデザインの実装
- フロントエンドテストの作成

## 使用技術
#[[file:../docs/frontend-stack.md]]

## コーディング規約
#[[file:./coding-standards.md]]

## デザインシステム
#[[file:../design-system/guidelines.md]]
```

### パターン4: 機能別Steering

```markdown
---
inclusion: fileMatch
fileMatchPattern: 'src/features/authentication/**/*'
---

# 認証機能開発ガイド

## セキュリティ要件
- パスワードは必ずbcryptでハッシュ化
- JWTトークンの有効期限は15分
- リフレッシュトークンは7日間有効
- CSRF対策を必ず実装

## API仕様
#[[file:../docs/auth-api-spec.yaml]]

## テスト要件
- 全ての認証フローをテスト
- セキュリティ脆弱性のテスト
- エッジケースのテスト

## 参考実装
#[[file:./examples/auth-implementation.ts]]
```

## 動的コンテンツの生成

### スクリプトによる生成

```bash
#!/bin/bash
# generate-steering.sh

# プロジェクト情報を収集
PROJECT_NAME=$(jq -r '.name' package.json)
VERSION=$(jq -r '.version' package.json)
DEPENDENCIES=$(jq -r '.dependencies | keys | join(", ")' package.json)

# Steeringファイルを生成
cat > .kiro/steering/00-project-info.md << EOF
---
inclusion: always
---

# プロジェクト情報（自動生成）

最終更新: $(date '+%Y-%m-%d %H:%M:%S')

## 基本情報
- プロジェクト名: ${PROJECT_NAME}
- バージョン: ${VERSION}
- 依存関係: ${DEPENDENCIES}

## 最近の変更
$(git log --oneline -5)

## アクティブなブランチ
$(git branch --show-current)
EOF

echo "Steeringファイルを生成しました"
```

### CI/CDでの自動更新

```yaml
# .github/workflows/update-steering.yml
name: Update Steering Files

on:
  push:
    branches: [ main ]
    paths:
      - 'package.json'
      - 'docs/**'

jobs:
  update-steering:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
    
    - name: Generate project info
      run: |
        bash scripts/generate-steering.sh
    
    - name: Commit changes
      run: |
        git config user.name "GitHub Actions"
        git config user.email "actions@github.com"
        git add .kiro/steering/
        git commit -m "chore: update steering files" || echo "No changes"
        git push
```

## ベストプラクティス

### 1. 明確な命名規則

```
# 良い例
.kiro/steering/
├── 00-project-basics.md
├── 10-coding-standards-typescript.md
├── 20-security-authentication.md
├── 30-frontend-react-components.md

# 悪い例
.kiro/steering/
├── file1.md
├── rules.md
├── stuff.md
```

### 2. 適切な粒度

```markdown
# 良い例: 適切な粒度
---
inclusion: fileMatch
fileMatchPattern: 'src/components/**/*.tsx'
---

# React コンポーネント規約

## 命名規則
- PascalCase を使用
- 機能を表す名前を付ける

## ファイル構造
- 1ファイル1コンポーネント
- 関連するスタイルは同じフォルダ

# 悪い例: 粒度が粗すぎる
---
inclusion: always
---

# 全ての開発ルール

（100ページ以上の内容）
```

### 3. バージョン管理

```markdown
---
inclusion: always
---

# コーディング規約

バージョン: 2.1.0
最終更新: 2024-01-15

## 変更履歴
- v2.1.0 (2024-01-15): TypeScript 5.0対応
- v2.0.0 (2023-12-01): ESLint設定の大幅変更
- v1.0.0 (2023-10-01): 初版
```

### 4. 例示の活用

```markdown
---
inclusion: fileMatch
fileMatchPattern: 'src/api/**/*.ts'
---

# API実装ガイド

## エラーハンドリング

### 良い例
```typescript
try {
  const user = await userService.getUser(id);
  return res.json({ success: true, data: user });
} catch (error) {
  if (error instanceof NotFoundError) {
    return res.status(404).json({
      success: false,
      error: { code: 'USER_NOT_FOUND', message: error.message }
    });
  }
  throw error;
}
```

### 悪い例
```typescript
const user = await userService.getUser(id);
res.json(user);  // エラーハンドリングなし
```
```

## トラブルシューティング

### 問題1: Steeringファイルが適用されない

**確認項目:**

```bash
# 1. ファイルの存在確認
ls -la .kiro/steering/

# 2. Front-matterの構文確認
head -5 .kiro/steering/your-file.md

# 3. YAMLの妥当性確認
python -c "import yaml; yaml.safe_load(open('.kiro/steering/your-file.md').read().split('---')[1])"
```

**よくある間違い:**

```markdown
# 間違い1: Front-matterの区切りが不正
--
inclusion: always
--

# 正しい
---
inclusion: always
---

# 間違い2: fileMatchPatternにクォートがない
---
inclusion: fileMatch
fileMatchPattern: src/**/*.ts
---

# 正しい
---
inclusion: fileMatch
fileMatchPattern: 'src/**/*.ts'
---
```

### 問題2: ファイル参照が解決されない

**確認項目:**

```bash
# 1. 参照ファイルの存在確認
ls -la docs/openapi.yaml

# 2. 相対パスの確認
# Steeringファイルの場所: .kiro/steering/api-guide.md
# 参照ファイルの場所: docs/openapi.yaml
# 正しい相対パス: ../../docs/openapi.yaml

# 3. パスの検証
realpath .kiro/steering/api-guide.md
realpath docs/openapi.yaml
```

### 問題3: パフォーマンスが低下

**原因と対策:**

```markdown
# 原因1: Steeringファイルが大きすぎる
# 対策: ファイルを分割

# 原因2: 参照ファイルが大きすぎる
# 対策: 必要な部分のみを抽出

# 原因3: 常に適用されるファイルが多すぎる
# 対策: 条件付き適用に変更

---
# 変更前
inclusion: always
---

# 変更後
inclusion: fileMatch
fileMatchPattern: 'src/specific/**/*.ts'
---
```

## まとめ

Steering高度な使用方法により：

1. **柔軟な設定管理**: 3つのinclusionモードの使い分け
2. **効率的な情報共有**: ファイル参照機能の活用
3. **保守性の向上**: 階層的で明確な構造
4. **チーム開発の促進**: 役割別・機能別の設定

> 💡 **推奨アプローチ**: シンプルな構成から始めて、必要に応じて段階的に高度な機能を追加していくことをお勧めします。

> 📖 **公式ドキュメント**: 最新の機能と詳細については [kiro.dev/docs](https://kiro.dev/docs/) を参照してください

---

## 📚 関連リソース

- [🏠 目次](../../README.md)
- [📋 Steering設計原則](../chapter2/steering-design-principles.md)
- [📁 Steering管理戦略](../chapter3/steering-management.md)
- [📁 Steeringテンプレート](../../templates/steering/)
- [🛠️ トラブルシューティング](../troubleshooting/common-issues.md)
