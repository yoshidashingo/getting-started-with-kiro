# Design Document

## Overview

Kiro解説ドキュメントは、https://kiro.dev/docs/ の最新情報に基づいた、初心者向けの包括的な学習リソースとして設計されます。ドキュメントは段階的な学習アプローチを採用し、基本概念から実践的な使用方法、高度な機能（Specs、Steering、Hooks、MCP）まで体系的に構成されます。日本語での分かりやすい説明と最新の実践的なサンプルを組み合わせることで、効果的な学習体験を提供します。

## Architecture

### ドキュメント構造
```
docs/
├── chapter1/                 # 第1章: はじめてのKiro
│   ├── kiro-introduction.md  # Kiroの基礎解説（最新版）
│   ├── tetris-tutorial.md    # テトリス作成チュートリアル
│   └── playwright-mcp-testing.md  # Playwright MCPテスト
├── chapter2/                 # 第2章: 本格的なアプリ開発
│   ├── ai-consultation.md    # AI相談とプロジェクト企画
│   ├── aws-mcp-setup.md      # AWS MCP設定
│   ├── steering-design-principles.md  # Steering設計原則
│   ├── pattern-language.md   # パターン言語解説
│   ├── design-review-implementation.md  # 設計・レビュー・CI/CD
│   ├── implementation-testing.md  # 実装・テスト・自動化
│   └── git-pr-workflow.md    # Git連携・PR・E2E
├── chapter3/                 # 第3章: チーム開発
│   ├── team-development-setup.md  # チーム開発セットアップ
│   ├── steering-management.md     # Steering管理戦略
│   └── context-memory-management.md  # コンテキスト・メモリ管理
├── features/                 # 機能詳細リファレンス（新規）
│   ├── autonomy-modes.md     # AutopilotとSupervisedモード
│   ├── chat-context.md       # Chat Context詳細
│   ├── specs-workflow.md     # Specsワークフロー詳細
│   ├── steering-advanced.md  # Steering高度な使用方法
│   ├── hooks-guide.md        # Hooks完全ガイド
│   └── mcp-configuration.md  # MCP設定完全ガイド
├── examples/                 # サンプルプロジェクト
│   ├── tetris-backup/        # テトリスゲーム完成版
│   ├── webapp-backup/        # Webアプリ完成版
│   └── mcp-examples/         # MCP設定例集（新規）
├── templates/                # テンプレート集
│   ├── mcp/                  # MCP設定テンプレート
│   ├── steering/             # Steeringテンプレート
│   └── cicd/                 # CI/CD設定テンプレート
└── troubleshooting/          # トラブルシューティング
    ├── common-issues.md      # よくある問題
    └── faq.md                # FAQ
```

### 学習フロー設計
1. **導入フェーズ（第1章）**: Kiroの概要と基本概念の理解、簡単なアプリ作成体験
2. **実践フェーズ（第2章）**: 本格的なアプリ開発、Specs/Steering/Hooks/MCPの活用
3. **協働フェーズ（第3章）**: チーム開発環境の構築と管理
4. **リファレンスフェーズ**: 各機能の詳細な技術情報の参照
5. **継続学習フェーズ**: 公式ドキュメントとの連携、最新情報の追跡

## Components and Interfaces

### ドキュメントコンポーネント

#### 1. 導入ドキュメント
- **目的**: Kiroの基本概念と価値提案の説明
- **内容**: 
  - Kiroの定義と目的
  - 主要機能の概要
  - 利用シーンと利点
- **形式**: Markdown形式、図解付き

#### 2. 機能解説ドキュメント
- **目的**: 各機能の最新の詳細な説明と使用方法
- **内容**:
  - 機能の概要と目的（公式ドキュメント準拠）
  - Autopilot/Supervisedモードの違いと使い分け
  - Chat Context（#File、#Folder、#Problems、#Terminal、#Git Diff、#Codebase）の活用
  - Specsワークフロー（要件→設計→タスク）の詳細
  - Steeringファイルの構造とfront-matter設定
  - Hooksのイベントトリガー設定
  - MCP設定（.kiro/settings/mcp.json、uvx使用方法）
  - 実践的なサンプルコードと設定例
  - ベストプラクティスと推奨事項
- **形式**: 機能別のMarkdownファイル、公式ドキュメントへのリンク

#### 3. チュートリアルドキュメント
- **目的**: 段階的な実践演習の提供
- **内容**:
  - ステップバイステップの手順
  - 期待される結果の明示
  - 演習用サンプルプロジェクト
- **形式**: 演習形式のMarkdownファイル

#### 4. サンプルプロジェクト
- **目的**: 実践的な学習材料の提供
- **内容**:
  - 完全に動作するサンプルコード
  - 詳細なコメントと説明
  - 段階的な実装手順
- **形式**: 実際のプロジェクトファイル

### ナビゲーション設計
- **階層構造**: 論理的な情報階層による整理
- **相互リンク**: 関連する内容への適切なリンク
- **進捗管理**: 学習進捗を追跡できる仕組み

## Data Models

### ドキュメントメタデータ
```yaml
title: ドキュメントタイトル
description: ドキュメントの説明
level: beginner|intermediate|advanced
prerequisites: 前提知識のリスト
estimated_time: 推定学習時間
tags: タグのリスト
```

### チュートリアル構造
```yaml
tutorial:
  title: チュートリアルタイトル
  overview: 概要
  objectives: 学習目標のリスト
  steps:
    - title: ステップタイトル
      description: ステップの説明
      code_example: サンプルコード
      expected_result: 期待される結果
  conclusion: まとめ
```

## Error Handling

### ドキュメント品質管理
- **リンク検証**: 内部・外部リンクの有効性確認
- **コード検証**: サンプルコードの動作確認
- **言語品質**: 日本語表現の自然さと正確性の確認

### ユーザビリティ対応
- **アクセシビリティ**: 読みやすさとナビゲーションの最適化
- **レスポンシブ対応**: 様々なデバイスでの閲覧対応
- **検索機能**: 効率的な情報検索の提供

## Testing Strategy

### ドキュメント検証
1. **内容検証**
   - 技術的正確性の確認
   - 手順の実行可能性テスト
   - サンプルコードの動作確認

2. **ユーザビリティテスト**
   - 初心者による実際の使用テスト
   - 学習効果の測定
   - フィードバック収集と改善

3. **品質保証**
   - 日本語表現の校正
   - 一貫性の確認
   - アクセシビリティチェック

### 継続的改善
- **フィードバック収集**: ユーザーからの意見収集機能
- **使用状況分析**: ドキュメント利用パターンの分析
- **定期更新**: Kiroの機能更新に合わせたドキュメント更新