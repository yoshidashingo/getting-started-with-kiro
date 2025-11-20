# Getting Started with Kiro

このリポジトリは、Kiroを初めて使用する方向けの包括的なチュートリアルとハンズオンガイドです。Kiroの基本概念から実践的な使用方法まで、段階的に学習できるように構成されています。

## 📚 学習目標

このチュートリアルを完了すると、以下のことができるようになります：

- **Kiroの基本概念とスペック駆動開発の理解** - AIコーディングのベストプラクティスを習得できる
- **Kiroを使った実際のアプリケーション開発** - テトリスから本格的なWebアプリまで開発を体験できる
- **チーム開発でのKiro活用方法** - チームでのコラボレーション開発とCI/CDパイプラインを統合した非同期開発・テストやデプロイが自動化できる
- **高度な機能（MCP、Steering、Hooks）の実践的な使用** - さらに便利で効率的な開発環境が構築できる

## 🎯 前提知識

このチュートリアルを始める前に、以下の知識があることを前提としています：

- **基本的なプログラミング知識** - 変数、関数、条件分岐などの基本概念
- **コマンドライン操作の基礎** - ターミナルでの基本的なコマンド実行
- **Gitの基本的な使用方法** - コミット、プッシュ、プルリクエストの概念

## ⏱️ 推定学習時間

| 章 | 内容 | 推定時間 | 難易度 |
|---|---|---|---|
| **第1章** | 基本概念とシンプルなアプリ作成 | 2-3時間 | 初級 |
| **第2章** | 本格的なアプリ開発と高度な機能 | 4-6時間 | 中級 |
| **第3章** | チーム開発の設定と管理 | 2-3時間 | 中級 |
| **合計** | | **8-12時間** | |

## 🚀 学習の進め方

### 推奨学習フロー
1. **順次学習**: 各章を順番に進めることを強く推奨します
2. **実践重視**: 各セクションの演習を必ず実際に行ってください
3. **復習**: 理解が不十分な部分は前の章に戻って復習してください

### 学習サポート
- **トラブルシューティング**: 問題が発生した場合は [よくある問題](docs/troubleshooting/common-issues.md) を確認
- **FAQ**: 疑問点は [FAQ](docs/troubleshooting/faq.md) で解決
- **サンプルコード**: [examples/](examples/) ディレクトリに完成版のコードを用意してあります

### 学習進捗の確認
各章の最後に「学習成果」が記載されています。これらの項目ができるようになったら次の章に進んでください。

#### 📊 進捗トラッキング
各ドキュメントの最後にある「学習進捗チェック」を活用して、自分の理解度を確認しましょう：

```
- [ ] 項目1: 理解できた
- [ ] 項目2: 実践できた  
- [ ] 項目3: 応用できた
```

すべてのチェック項目が完了したら、次のセクションに進むことをお勧めします。

---

## 📖 目次とナビゲーション

### 🌟 第1章: はじめてのKiro
- [1.1 Kiroの基礎解説](docs/chapter1/kiro-introduction.md) - Kiroの基本概念とインストール
- [1.2 テトリスを作ってみよう](docs/chapter1/tetris-tutorial.md) - 実践的なアプリ開発体験
- [1.3 Playwright MCPでテストしてみよう](docs/chapter1/playwright-mcp-testing.md) - 自動テストの基礎

### 🚀 第2章: 本格的なアプリを作ろう
- [2.1 なにを作るかAIに相談してみよう](docs/chapter2/ai-consultation.md) - AI活用法
- [2.2 AWS MCP設定](docs/chapter2/aws-mcp-setup.md) - 外部サービス連携
- [2.3 Steering設計原則](docs/chapter2/steering-design-principles.md) - プロジェクト固有の設計指針
- [2.4 パターン言語解説](docs/chapter2/pattern-language.md) - 再利用可能な設計パターン
- [2.5 設計・レビュー・CI/CD](docs/chapter2/design-review-implementation.md) - 体系的な開発プロセス
- [2.6 実装・テスト・自動化](docs/chapter2/implementation-testing.md) - 実践的な開発サイクル
- [2.7 Git連携・PR・E2E](docs/chapter2/git-pr-workflow.md) - チーム開発の基礎

### 👥 第3章: チーム開発を始めよう
- [3.1-3.2 チーム開発セットアップ](docs/chapter3/team-development-setup.md) - 協働開発環境の構築
- [3.3 Steering管理戦略](docs/chapter3/steering-management.md) - チーム設定の管理
- [3.4 コンテキスト・メモリ管理](docs/chapter3/context-memory-management.md) - 大規模開発のテクニック

### 🔧 機能詳細リファレンス
- [Autonomy Modes完全ガイド](docs/features/autonomy-modes.md) - AutopilotとSupervisedモードの詳細
- [Chat Context完全ガイド](docs/features/chat-context.md) - 6つのコンテキスト機能の活用
- [Specsワークフロー完全ガイド](docs/features/specs-workflow.md) - 要件→設計→タスクの詳細プロセス
- [Steering高度な使用方法ガイド](docs/features/steering-advanced.md) - Steeringの高度な機能
- [Hooks完全ガイド](docs/features/hooks-guide.md) - イベントトリガー自動化
- [MCP設定完全ガイド](docs/features/mcp-configuration.md) - MCP設定の詳細

### 🛠️ サポートリソース
- [よくある問題](docs/troubleshooting/common-issues.md) - トラブルシューティングガイド
- [FAQ](docs/troubleshooting/faq.md) - よくある質問と回答
- [サンプルプロジェクト](examples/) - 完成版のコード例
- [MCP設定例](examples/mcp-examples/) - MCP設定例集
- [テンプレート](templates/) - 設定ファイルのテンプレート

---

## 1章 はじめてのKiro

**学習目標**: Kiroの基本概念を理解し、簡単なアプリケーションを作成できるようになる  
**推定時間**: 2-3時間

### 1.1 Kiro 解説
📖 **[詳細ガイド](docs/chapter1/kiro-introduction.md)**

- Kiroは簡単に始められ、AIコーディングのベストプラクティスの1つであるスペック駆動開発を、強力なガイド機能に沿って実践できます
- Kiroはkiro.devからダウンロードできます
- Kiroのスペック駆動開発は、要件作成、設計、タスク分割・遂行の3段階です
- **学習成果**: Kiroをインストールして使い始めることができる。開発の基本的な流れを説明するための用語や段取りを理解する

### 1.2 Kiroを使ってテトリスを作ってみよう
🎮 **[詳細ガイド](docs/chapter1/tetris-tutorial.md)**

- Kiroを使って一発でテトリスを作成してみましょう
- ローカルサーバーを起動してみて試す
- 簡単な要求・設計の修正をする
- **学習成果**: 実際に動作するアプリケーションをどのような手順で作成すればよいか理解する

### 1.3 Playwright MCPでテストしてみよう
🧪 **[詳細ガイド](docs/chapter1/playwright-mcp-testing.md)**

- MCPの設定のしかた
- テストの作成
- テストの実施
- **学習成果**: MCPの概念を理解し、自動テストの基礎を身につける

## 2章 本格的なアプリを作ろう

**学習目標**: 実践的なWebアプリケーションを開発し、Kiroの高度な機能を活用できるようになる  
**推定時間**: 4-6時間

### 2.1 作りたいものをAIに相談しよう
💡 **[詳細ガイド](docs/chapter2/ai-consultation.md)**

- AIとの効果的な相談方法
- プロジェクト企画のベストプラクティス
- **学習成果**: AIを活用した効率的なプロジェクト企画ができるようになる

### 2.2 MCPを設定しよう > AWSドキュメント系
⚙️ **[詳細ガイド](docs/chapter2/aws-mcp-setup.md)**

- AWSドキュメント系MCPの設定手順
- 実際の設定例とトラブルシューティング
- **学習成果**: MCPを使ってAWSサービスの情報を効率的に活用できる

### 2.3 Steeringファイルに設計原則を定義しよう
📋 **[詳細ガイド](docs/chapter2/steering-design-principles.md)**

- Steeringファイルの概念と作成方法
- 設計原則の定義方法と実例
- **学習成果**: プロジェクト固有の設計原則を定義し、一貫した開発ができる

### 2.4 設計原則に必要なパタン言語の解説を作ろう
🏗️ **[詳細ガイド](docs/chapter2/pattern-language.md)**

- 設計パターンの基本概念
- Kiroでの活用方法と具体例
- **学習成果**: 設計パターンを理解し、再利用可能な設計ができる

### 2.5 設計ファイルを効率的に作成・レビュー・CI/CD構築
📝 **[詳細ガイド](docs/chapter2/design-review-implementation.md)**

- 設計ファイル作成からタスクリストレビューまでの流れ
- AIとの協働による設計レビュー方法
- タスクリストの作成と管理
- CI/CDパイプラインの構築と自動化
- **学習成果**: 体系的な設計プロセスとCI/CD統合を実践できる

### 2.6 アプリを実装・テスト・自動化しよう
💻 **[詳細ガイド](docs/chapter2/implementation-testing.md)**

- アプリ実装の段階的手順
- ローカル実行と修正のサイクル
- 継続的なテストと改善プロセス
- Hooksを使ったUnit Test自動化
- **学習成果**: 実際のアプリケーション開発プロセスを体験できる

### 2.7 Git連携・PR・E2Eテストを実践しよう
📤 **[詳細ガイド](docs/chapter2/git-pr-workflow.md)**

- コミット・Push・PR作成の手順
- AIによるPRレビューの活用方法
- Playwright MCPでのE2Eテスト実装
- チーム開発ワークフローの完成
- **学習成果**: Git連携とPRワークフローを習得できる



## 3章 チーム開発を始めよう

**学習目標**: チーム開発環境でのKiro活用方法を習得し、効率的な協働開発ができるようになる  
**推定時間**: 2-3時間

### 3.1 GitHubリポジトリを作成してチーム開発を始めよう
🤝 **[詳細ガイド](docs/chapter3/team-development-setup.md)**

- GitHubリポジトリの作成とチーム設定
- チーム開発のワークフロー構築
- **学習成果**: チーム開発環境を構築し、協働開発を開始できる

### 3.2 Amazon Q Developer と GitHub Actions ワークフローと統合する
🔗 **[上記ガイドに含まれます](docs/chapter3/team-development-setup.md)**

- CI/CDパイプラインとの統合方法
- 自動化ワークフローの設定
- **学習成果**: 継続的インテグレーションを活用した開発プロセスを構築できる

### 3.3 Steeringファイルの管理戦略
📁 **[詳細ガイド](docs/chapter3/steering-management.md)**

- ローカルとプロジェクト共用のSteeringファイル管理
- チーム開発でのベストプラクティス
- **学習成果**: ローカルとプロジェクト共用のSteeringファイル管理戦略を実践できる

### 3.4 コンテキスト制御とメモリ管理
🧠 **[詳細ガイド](docs/chapter3/context-memory-management.md)**

- コンテキスト制御の方法とメモリ管理
- 大規模プロジェクトでの効率的な開発手法
- **学習成果**: 大規模開発でのKiro活用テクニックを習得できる

---

## 💡 プロジェクトの使用方法

### 初回セットアップ
1. **Kiroのインストール**: [kiro.dev](https://kiro.dev) からKiroをダウンロード・インストール
2. **リポジトリのクローン**: このリポジトリをローカルにクローン
3. **第1章から開始**: [Kiro解説](docs/chapter1/kiro-introduction.md) から学習を開始

### 学習の進め方
- **段階的学習**: 各章を順番に進める
- **実践重視**: サンプルコードを実際に動かす
- **復習**: 理解が不十分な部分は繰り返し学習

### ファイル構成
```
├── docs/                    # メインドキュメント
│   ├── chapter1/           # 第1章: 基礎編
│   ├── chapter2/           # 第2章: 実践編  
│   ├── chapter3/           # 第3章: チーム開発編
│   └── troubleshooting/    # トラブルシューティング
├── examples/               # サンプルプロジェクト
│   ├── tetris-backup/     # テトリスゲーム完成版
│   └── webapp-backup/     # Webアプリ完成版
├── templates/              # 設定ファイルテンプレート
│   ├── mcp/               # MCP設定例
│   ├── steering/          # Steering設定例
│   └── cicd/              # CI/CD設定例
└── scripts/               # 検証・テストスクリプト
```

## 🎯 次のステップ

このチュートリアルを完了したら、以下のリソースを活用してさらに学習を深めてください：

### 公式リソース
- 📖 [Kiro公式ドキュメント](https://kiro.dev) - 最新の機能と詳細な仕様
- 💬 [コミュニティフォーラム](https://community.kiro.dev) - 質問と情報交換
- 🔧 [GitHub Issues](https://github.com/kiro-dev/kiro/issues) - バグレポートと機能要望

### 実践プロジェクト
- 🎮 [テトリスゲーム](examples/tetris-backup/) - 完成版のコード参考
- 🌐 [Webアプリケーション](examples/webapp-backup/) - 実践的なアプリ開発例
- 📋 [設定テンプレート](templates/) - プロジェクト開始時の参考資料

## 🤝 貢献について

このチュートリアルの改善にご協力いただける場合は、以下の方法でご参加ください：

- **バグ報告**: 間違いや問題を発見した場合はIssueを作成
- **改善提案**: より良い説明方法や新しいトピックの提案
- **翻訳**: 他言語への翻訳協力
- **サンプル追加**: 新しいサンプルプロジェクトの提供

Pull Requestやフィードバックをお気軽にお送りください！

---

**📝 最終更新**: 2025年11月  
**🏷️ バージョン**: v2.0  
**📖 公式ドキュメント**: [kiro.dev/docs](https://kiro.dev/docs/)  
**📧 お問い合わせ**: [GitHub Issues](https://github.com/yoshidashingo/getting-started-with-kiro/issues) でお気軽にどうぞ
