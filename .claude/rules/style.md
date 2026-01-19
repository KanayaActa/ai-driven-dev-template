# スタイルルール

## コード
- 不変性（Immutability）を重視
- 関数は小さく保つ（50行以下推奨）
- 早期リターンを使用（ネストを減らす）
- マジックナンバーは定数化

## 命名
- 変数/関数: camelCase
- 定数: UPPER_SNAKE_CASE
- コンポーネント: PascalCase
- ファイル: kebab-case

## コメント
- 絵文字は使用しない
- 日本語コメント可
- WHYを書く、WHATは書かない（コードを読めばわかる）

## フォーマット
- .prettierrc に従う（Single Source of Truth）
- インデント: 2スペース
- セミコロン: なし
- クォート: シングル
