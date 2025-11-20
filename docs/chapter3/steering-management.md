# Steeringファイル管理戦略ガイド

## 概要

Steeringファイルは、Kiroの動作をカスタマイズし、チーム開発における一貫性を保つための重要な仕組みです。このガイドでは、ローカル環境とプロジェクト共用のSteeringファイルの効果的な管理方法と、チーム開発でのベストプラクティスについて詳しく説明します。

## Steeringファイルとは

### 基本概念

Steeringファイルは、Kiroに対して追加のコンテキストや指示を提供するMarkdownファイルです。これにより、プロジェクト固有のルールや標準を自動的に適用できます。

### 主な用途

- **コーディング規約の自動適用**
- **プロジェクト固有のベストプラクティスの共有**
- **アーキテクチャガイドラインの統一**
- **チーム開発ルールの標準化**

## 1. Steeringファイルの配置戦略

### 1.1 ファイル配置の基本構造

```
.kiro/steering/
├── always-included/          # 常に適用されるファイル
│   ├── coding-standards.md   # コーディング規約
│   ├── security-guidelines.md # セキュリティガイドライン
│   └── project-context.md    # プロジェクト基本情報
├── conditional/              # 条件付きで適用されるファイル
│   ├── frontend-rules.md     # フロントエンド固有のルール
│   ├── backend-rules.md      # バックエンド固有のルール
│   └── testing-guidelines.md # テスト関連のガイドライン
└── manual/                   # 手動で呼び出すファイル
    ├── deployment-guide.md   # デプロイメントガイド
    ├── troubleshooting.md    # トラブルシューティング
    └── performance-tips.md   # パフォーマンス最適化
```

### 1.2 ローカル vs プロジェクト共用の使い分け

#### ローカル設定（~/.kiro/steering/）
```markdown
<!-- ~/.kiro/steering/personal-preferences.md -->
---
inclusion: always
---

# 個人的な開発設定

## エディタ設定
- インデントはスペース2つを使用
- 行末の空白は自動削除
- ファイル末尾に改行を追加

## 個人的なコーディングスタイル
- 変数名は camelCase を使用
- 関数名は動詞から始める
- コメントは日本語で記述
```

#### プロジェクト共用設定（.kiro/steering/）
```markdown
<!-- .kiro/steering/project-standards.md -->
---
inclusion: always
---

# プロジェクト開発標準

## アーキテクチャ原則
- Clean Architecture パターンを採用
- 依存性注入を積極的に活用
- 単一責任の原則を遵守

## API設計ガイドライン
- RESTful API設計を基本とする
- エラーレスポンスは統一フォーマットを使用
- バージョニングはURLパスで管理

#[[file:../docs/api-specification.yaml]]
```

## 2. 条件付き適用の設定

### 2.1 ファイルマッチングによる条件適用

```markdown
<!-- .kiro/steering/frontend-specific.md -->
---
inclusion: fileMatch
fileMatchPattern: 'src/components/**/*.tsx'
---

# React コンポーネント開発ガイドライン

## コンポーネント設計原則
- 単一責任の原則を遵守
- Props の型定義を必須とする
- デフォルトプロパティを適切に設定

## ファイル命名規則
- コンポーネントファイルは PascalCase
- スタイルファイルは kebab-case
- テストファイルは `.test.tsx` 拡張子

## 実装例
```tsx
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
}

export const Button: React.FC<ButtonProps> = ({
  label,
  onClick,
  variant = 'primary'
}) => {
  return (
    <button 
      className={`btn btn-${variant}`}
      onClick={onClick}
    >
      {label}
    </button>
  );
};
```
```

### 2.2 手動呼び出し用ファイルの設定

```markdown
<!-- .kiro/steering/deployment-procedures.md -->
---
inclusion: manual
---

# デプロイメント手順書

## 事前チェックリスト
- [ ] 全てのテストが通過していること
- [ ] セキュリティスキャンが完了していること
- [ ] パフォーマンステストが実施済みであること
- [ ] ドキュメントが更新されていること

## ステージング環境デプロイ
```bash
# 環境変数の設定
export ENVIRONMENT=staging
export DATABASE_URL=staging_db_url

# デプロイスクリプトの実行
npm run deploy:staging

# 動作確認
npm run test:e2e:staging
```

## 本番環境デプロイ
```bash
# 本番環境への切り替え
export ENVIRONMENT=production

# データベースマイグレーション
npm run db:migrate:production

# 本番デプロイ
npm run deploy:production

# ヘルスチェック
curl -f https://api.example.com/health
```
```

## 3. チーム開発でのベストプラクティス

### 3.1 Steeringファイルのバージョン管理

1. **Git管理の基本原則**
   ```bash
   # プロジェクト共用ファイルはGitで管理
   git add .kiro/steering/
   git commit -m "feat: add coding standards steering file"
   
   # ローカル設定ファイルは.gitignoreに追加
   echo "~/.kiro/steering/" >> ~/.gitignore
   ```

2. **ブランチ戦略との連携**
   ```bash
   # フィーチャーブランチでのSteering更新
   git checkout -b feature/update-coding-standards
   
   # Steeringファイルの更新
   vim .kiro/steering/coding-standards.md
   
   # 変更をコミット
   git add .kiro/steering/coding-standards.md
   git commit -m "docs: update coding standards for new framework"
   ```

### 3.2 チーム間での設定共有

1. **設定ファイルテンプレートの作成**
   ```markdown
   <!-- templates/steering-template.md -->
   ---
   inclusion: always
   ---
   
   # [プロジェクト名] 開発ガイドライン
   
   ## プロジェクト概要
   - プロジェクト名: [PROJECT_NAME]
   - 技術スタック: [TECH_STACK]
   - 開発期間: [TIMELINE]
   
   ## 開発ルール
   ### コーディング規約
   - [具体的なルールを記述]
   
   ### テスト戦略
   - [テスト方針を記述]
   
   ### デプロイメント
   - [デプロイ手順を記述]
   
   ## 外部リソース参照
   #[[file:../docs/architecture-decision-records.md]]
   #[[file:../docs/api-documentation.yaml]]
   ```

2. **新メンバーのオンボーディング**
   ```bash
   # 新メンバー用セットアップスクリプト
   #!/bin/bash
   
   echo "Kiro Steering ファイルのセットアップを開始します..."
   
   # プロジェクト固有の設定を確認
   if [ -d ".kiro/steering" ]; then
     echo "プロジェクト固有のSteering設定が見つかりました:"
     find .kiro/steering -name "*.md" -exec basename {} \;
   fi
   
   # 個人設定のテンプレートをコピー
   mkdir -p ~/.kiro/steering
   cp templates/personal-steering-template.md ~/.kiro/steering/personal-preferences.md
   
   echo "セットアップが完了しました。~/.kiro/steering/personal-preferences.md を編集してください。"
   ```

### 3.3 設定の一貫性管理

1. **設定検証スクリプト**
   ```bash
   #!/bin/bash
   # validate-steering.sh
   
   echo "Steeringファイルの検証を開始..."
   
   # 必須ファイルの存在確認
   required_files=(
     ".kiro/steering/coding-standards.md"
     ".kiro/steering/security-guidelines.md"
     ".kiro/steering/project-context.md"
   )
   
   for file in "${required_files[@]}"; do
     if [ ! -f "$file" ]; then
       echo "エラー: 必須ファイル $file が見つかりません"
       exit 1
     fi
   done
   
   # Markdownファイルの構文チェック
   find .kiro/steering -name "*.md" -exec markdownlint {} \;
   
   echo "検証が完了しました。"
   ```

2. **CI/CDでの自動検証**
   ```yaml
   # .github/workflows/steering-validation.yml
   name: Steering Files Validation
   
   on:
     pull_request:
       paths:
         - '.kiro/steering/**'
   
   jobs:
     validate-steering:
       runs-on: ubuntu-latest
       
       steps:
       - uses: actions/checkout@v4
       
       - name: Install markdownlint
         run: npm install -g markdownlint-cli
       
       - name: Validate steering files
         run: |
           # Markdownの構文チェック
           markdownlint .kiro/steering/**/*.md
           
           # 必須ファイルの存在確認
           bash scripts/validate-steering.sh
       
       - name: Check for broken references
         run: |
           # ファイル参照の検証
           grep -r "#\[\[file:" .kiro/steering/ | while read -r line; do
             file_ref=$(echo "$line" | sed -n 's/.*#\[\[file:\([^]]*\)\]\].*/\1/p')
             if [ ! -f "$file_ref" ]; then
               echo "エラー: 参照ファイル $file_ref が見つかりません"
               exit 1
             fi
           done
   ```

## 4. 高度な活用方法

### 4.1 動的コンテンツの参照

```markdown
<!-- .kiro/steering/api-integration.md -->
---
inclusion: fileMatch
fileMatchPattern: 'src/api/**/*.ts'
---

# API統合ガイドライン

## OpenAPI仕様の参照
最新のAPI仕様は以下を参照してください：

#[[file:../docs/openapi.yaml]]

## 認証方式
- JWT トークンベース認証を使用
- リフレッシュトークンの実装を必須とする
- トークンの有効期限は24時間

## エラーハンドリング
```typescript
interface ApiError {
  code: string;
  message: string;
  details?: Record<string, any>;
}

const handleApiError = (error: ApiError): void => {
  console.error(`API Error [${error.code}]: ${error.message}`);
  // エラー処理ロジック
};
```
```

### 4.2 環境別設定の管理

```markdown
<!-- .kiro/steering/environment-config.md -->
---
inclusion: always
---

# 環境別設定ガイド

## 開発環境
- デバッグログを有効化
- ホットリロードを使用
- モックAPIを利用可能

## ステージング環境
- 本番に近い設定を使用
- パフォーマンス監視を有効化
- E2Eテストを実行

## 本番環境
- エラーログのみ出力
- セキュリティヘッダーを強化
- 監視とアラートを設定

## 環境変数の管理
```bash
# .env.example
NODE_ENV=development
API_BASE_URL=https://api.example.com
DATABASE_URL=postgresql://localhost:5432/myapp
JWT_SECRET=your-secret-key
```
```

### 4.3 プロジェクト固有のツール統合

```markdown
<!-- .kiro/steering/tooling-integration.md -->
---
inclusion: always
---

# ツール統合ガイド

## 使用ツール一覧
- **Linter**: ESLint + Prettier
- **Testing**: Jest + React Testing Library
- **Build**: Vite
- **Deployment**: Docker + Kubernetes

## 開発ワークフロー
1. コード作成時はKiroのスペック機能を活用
2. 実装前に設計レビューを実施
3. テスト駆動開発を基本とする
4. コードレビューは必須

## 自動化されたチェック
- Pre-commit hooks でコード品質を保証
- CI/CD パイプラインでテストを実行
- セキュリティスキャンを定期実行

#[[file:../scripts/setup-dev-environment.sh]]
#[[file:../.eslintrc.js]]
#[[file:../jest.config.js]]
```

## 5. トラブルシューティング

### 5.1 よくある問題と解決方法

1. **Steeringファイルが適用されない**
   ```bash
   # 設定の確認
   ls -la .kiro/steering/
   
   # ファイルの内容確認
   head -10 .kiro/steering/your-file.md
   
   # Front-matter の構文確認
   grep -A 5 "^---$" .kiro/steering/your-file.md
   ```

2. **ファイル参照が解決されない**
   ```bash
   # 参照ファイルの存在確認
   find . -name "referenced-file.md"
   
   # 相対パスの確認
   realpath .kiro/steering/your-file.md
   realpath docs/referenced-file.md
   ```

3. **条件付き適用が機能しない**
   ```markdown
   <!-- 正しい設定例 -->
   ---
   inclusion: fileMatch
   fileMatchPattern: 'src/**/*.ts'
   ---
   
   <!-- 間違った設定例 -->
   ---
   inclusion: fileMatch
   fileMatchPattern: src/**/*.ts  # クォートが必要
   ---
   ```

### 5.2 パフォーマンス最適化

1. **大きなファイルの分割**
   ```bash
   # 大きなSteeringファイルを機能別に分割
   split -l 100 large-steering-file.md small-steering-
   ```

2. **不要なファイルの除外**
   ```markdown
   <!-- 条件を厳密に設定 -->
   ---
   inclusion: fileMatch
   fileMatchPattern: 'src/components/**/*.tsx'  # 特定のディレクトリのみ
   ---
   ```

## まとめ

効果的なSteeringファイル管理により、チーム開発の品質と効率を大幅に向上させることができます。重要なポイントは：

- **階層的な設定管理**: ローカル（`~/.kiro/steering/`）とプロジェクト（`.kiro/steering/`）の設定を適切に分離
- **条件付き適用の活用**: `inclusion: fileMatch`と`fileMatchPattern`でファイルタイプや状況に応じた柔軟な設定
- **ファイル参照機能**: `#[[file:<relative_file_name>]]`構文で外部ファイルを低摩擦で活用
- **バージョン管理との統合**: 設定変更の履歴管理と共有
- **継続的な改善**: チームの成長に合わせた設定の見直し

> 📖 **公式ドキュメント**: Steeringの詳細な仕様については [kiro.dev/docs](https://kiro.dev/docs/) を参照してください

次のステップとして、[コンテキスト制御とメモリ管理ガイド](context-memory-management.md)で、大規模プロジェクトでの効率的な開発手法について学習することをお勧めします。---

## 
📚 学習進捗チェック

このセクションを完了したら、以下の項目ができるようになっているか確認してください：

- [ ] ローカルとプロジェクト共用のSteeringファイル管理ができる
- [ ] チーム開発でのベストプラクティスを実践できる
- [ ] Steeringファイルの効果的な管理戦略を構築できる
- [ ] チーム内での設定統一ができる
- [ ] 継続的な改善プロセスを実装できる

---

<div align="center">

| [← 🤝 チーム開発セットアップ](team-development-setup.md) | [🏠 目次](../../README.md) | [🧠 コンテキスト・メモリ管理 →](context-memory-management.md) |
|:---:|:---:|:---:|

</div>

---

### 🔗 関連リソース
- [📁 Steeringテンプレート](../../templates/steering/)
- [📋 Steering設計原則](../chapter2/steering-design-principles.md)
- [🛠️ トラブルシューティング](../troubleshooting/common-issues.md)