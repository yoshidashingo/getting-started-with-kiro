---
inclusion: fileMatch
fileMatchPattern: 'src/**/*.{ts,tsx}'
---

# TypeScript/React 開発ガイドライン

このファイルは、src/配下の.tsまたは.tsxファイルを
編集する時のみ適用されます。

## 命名規則
- 変数・関数: camelCase
- クラス・コンポーネント: PascalCase
- 定数: UPPER_SNAKE_CASE
- ファイル名: kebab-case

## TypeScript規約
- 明示的な型注釈を使用
- `any`型の使用を避ける
- インターフェースを優先（typeよりも）
- 厳格モードを有効化

## React規約
- 関数コンポーネントを使用
- Hooksを活用
- Props の型定義を必須とする
- デフォルトプロパティを適切に設定

## 実装例

```typescript
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
