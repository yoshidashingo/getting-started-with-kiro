# Requirements Document

## Introduction

このプロジェクトは、Kiroを初めて使用するユーザー向けの包括的な解説ドキュメントを最新の公式情報（https://kiro.dev/docs/）に基づいて更新・作成することを目的としています。ドキュメントはKiroの基本概念、最新の主要機能、実践的な使用方法を分かりやすく説明し、初心者が効率的にKiroを学習できるようにします。特に、Autopilot/Supervisedモード、Specs、Chat Context、Steering、Hooks、MCPなどの最新機能を網羅します。

## Requirements

### Requirement 1

**User Story:** Kiroを初めて使うユーザーとして、Kiroの基本概念と全体像を理解したいので、分かりやすい概要ドキュメントが欲しい

#### Acceptance Criteria

1. WHEN ユーザーがドキュメントを開いた時 THEN システムは Kiroの定義と目的を明確に説明する
2. WHEN ユーザーが概要を読む時 THEN システムは Kiroの主要な特徴と利点を箇条書きで提示する
3. WHEN ユーザーが全体像を把握したい時 THEN システムは Kiroの基本的なワークフローを図解で説明する

### Requirement 2

**User Story:** 開発者として、Kiroの具体的な機能を理解したいので、各機能の詳細な説明とサンプルが欲しい

#### Acceptance Criteria

1. WHEN ユーザーが機能一覧を確認する時 THEN システムは 各主要機能（Autopilot、Supervised、Chat Context、Steering、Spec、Hooks、MCP）の最新の説明を公式ドキュメントに基づいて提供する
2. WHEN ユーザーが特定の機能を学習する時 THEN システムは その機能の使用方法を最新の具体例付きで説明する
3. WHEN ユーザーが実践的な使い方を知りたい時 THEN システムは 各機能のベストプラクティスと最新の推奨事項を提示する
4. WHEN ユーザーがAutopilotとSupervisedモードの違いを理解したい時 THEN システムは 両モードの特徴と使い分けを明確に説明する
5. WHEN ユーザーがChat Contextの活用方法を知りたい時 THEN システムは #File、#Folder、#Problems、#Terminal、#Git Diff、#Codebaseなどのコンテキスト機能を詳細に解説する

### Requirement 3

**User Story:** 初心者として、Kiroを実際に使い始めるための手順を知りたいので、ステップバイステップのガイドが欲しい

#### Acceptance Criteria

1. WHEN ユーザーがセットアップを開始する時 THEN システムは 初期設定の手順を順序立てて説明する
2. WHEN ユーザーが最初のプロジェクトを作成する時 THEN システムは 基本的な操作手順を段階的に提示する
3. WHEN ユーザーが困った時 THEN システムは よくある問題とその解決方法を提供する

### Requirement 4

**User Story:** 学習者として、実際にKiroを体験したいので、簡単なハンズオン形式のチュートリアルが欲しい

#### Acceptance Criteria

1. WHEN ユーザーがハンズオンを開始する時 THEN システムは 実践的な演習課題を提供する
2. WHEN ユーザーが演習を進める時 THEN システムは 各ステップの期待される結果を明示する
3. WHEN ユーザーが演習を完了する時 THEN システムは 学習成果を確認できる方法を提供する

### Requirement 5

**User Story:** 日本語ユーザーとして、母国語でKiroを学習したいので、日本語で書かれた分かりやすいドキュメントが欲しい

#### Acceptance Criteria

1. WHEN ユーザーがドキュメントを読む時 THEN システムは 全ての内容を自然な日本語で提供する
2. WHEN ユーザーが技術用語を理解する時 THEN システムは 専門用語に適切な日本語訳と説明を併記する
3. WHEN ユーザーがサンプルコードを確認する時 THEN システムは コメントや説明を日本語で記述する

### Requirement 6

**User Story:** Kiroの高度な機能を活用したい開発者として、Specs、Steering、Hooks、MCPの詳細な使用方法を理解したいので、実践的なガイドが欲しい

#### Acceptance Criteria

1. WHEN ユーザーがSpecsの使い方を学習する時 THEN システムは 要件定義、設計、タスク実装の3段階のワークフローを詳細に説明する
2. WHEN ユーザーがSteeringファイルを作成する時 THEN システムは .kiro/steering/*.mdの構造、front-matter設定（inclusion: always/fileMatch/manual）、ファイル参照方法を解説する
3. WHEN ユーザーがHooksを設定する時 THEN システムは イベントトリガー型の自動化（保存時のテスト実行など）の実装方法を提供する
4. WHEN ユーザーがMCPを設定する時 THEN システムは .kiro/settings/mcp.jsonと~/.kiro/settings/mcp.jsonの設定方法、uvxコマンドの使用方法、autoApprove設定を説明する
5. WHEN ユーザーがMCPサーバーをテストする時 THEN システムは 設定確認前に直接ツールを試す方法を推奨する

### Requirement 7

**User Story:** チーム開発を行う開発者として、Kiroを使った協働開発の方法を理解したいので、チーム開発のベストプラクティスが欲しい

#### Acceptance Criteria

1. WHEN ユーザーがチーム開発を開始する時 THEN システムは ワークスペースレベルとユーザーレベルの設定の違いと使い分けを説明する
2. WHEN ユーザーがSteeringファイルを共有する時 THEN システムは プロジェクト共通の設定とローカル設定の管理方法を提供する
3. WHEN ユーザーがMCP設定を管理する時 THEN システムは ワークスペース設定とユーザー設定のマージ方法と優先順位を解説する
4. WHEN ユーザーがCI/CD統合を行う時 THEN システムは GitHub ActionsやAmazon Q Developerとの統合方法を説明する