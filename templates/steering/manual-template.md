---
inclusion: manual
---

# デプロイメント手順書

このファイルは、チャットで明示的に参照した時のみ読み込まれます。

使用方法: #Steering deployment-procedures

## 事前チェックリスト
- [ ] 全てのテストが通過していること
- [ ] セキュリティスキャンが完了していること
- [ ] パフォーマンステストが実施済みであること
- [ ] ドキュメントが更新されていること
- [ ] 変更ログが記録されていること

## ステージング環境デプロイ

### 1. 環境変数の設定
```bash
export ENVIRONMENT=staging
export DATABASE_URL=staging_db_url
export API_KEY=staging_api_key
```

### 2. ビルドの作成
```bash
npm run build:staging
```

### 3. デプロイの実行
```bash
npm run deploy:staging
```

### 4. 動作確認
```bash
npm run test:e2e:staging
curl -f https://staging.example.com/health
```

## 本番環境デプロイ

### 1. 最終確認
- ステージング環境での動作確認完了
- チームメンバーの承認取得
- バックアップの作成完了

### 2. 本番環境への切り替え
```bash
export ENVIRONMENT=production
```

### 3. データベースマイグレーション
```bash
npm run db:migrate:production
```

### 4. 本番デプロイ
```bash
npm run deploy:production
```

### 5. ヘルスチェック
```bash
curl -f https://api.example.com/health
npm run test:smoke:production
```

### 6. 監視の確認
- ログの確認
- メトリクスの確認
- アラートの設定確認

## ロールバック手順

問題が発生した場合の緊急対応：

```bash
# 前のバージョンにロールバック
npm run rollback:production

# データベースのロールバック（必要に応じて）
npm run db:rollback:production

# 動作確認
curl -f https://api.example.com/health
```

## トラブルシューティング

### デプロイが失敗する
1. ログを確認
2. 環境変数を確認
3. 権限を確認
4. ネットワーク接続を確認

### ヘルスチェックが失敗する
1. サービスの起動状態を確認
2. データベース接続を確認
3. 依存サービスの状態を確認
