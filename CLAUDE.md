# CLAUDE.md — [プロジェクト名]

## 概要
[1行でプロジェクトを説明]

## 初期セットアップ時の注意
- `.github/workflows/ci.yml` の `on: push/pull_request` はコメントアウトされています。プロジェクト作成後に必ずコメントを外してCIを有効化してください。

## コマンド
- pnpm dev      # 開発サーバー
- pnpm test     # テスト実行
- pnpm lint     # リント
- pnpm build    # ビルド

## 設定ファイル（Single Source of Truth）
- フォーマット: .prettierrc
- リント: .eslintrc.json
- TypeScript: tsconfig.json
※ エディタ、Hooks、CI すべてこれらを参照すること

## コード規約
- Conventional Commits (feat/fix/docs/refactor/test)
- 小さな差分を優先（大規模リファクタは避ける）
- 不変性（Immutability）を重視
- 絵文字は使用しない

## セキュリティ規約
- ハードコードされた秘密鍵を禁止
- 入力値の検証を必須化
- console.log は本番コードに残さない

## テスト規約
- カバレッジ80%以上を目標
- 変更したロジックには必ずテストを追加

## Linear連携
- 接頭辞: [YOUR_PREFIX]
- ステータス: Todo → In Progress → In Review → Done
- Security Issue: Priority: Urgent で管理

## 復帰時の確認事項
- Linear で現在のタスクを確認
- gh pr view で進捗を確認
- /resume でコンテキストを復元

## CI/品質対応フロー
- CI完了は待機しない（Fire and Forget）。
- CI失敗通知が来たら `/handle-ci-failure` を実行。
- エラーは即時修正せず、必ずLinearのチケットとして起票してから着手する。

## 過去の学習（自己修正で蓄積）
<!-- /update-memory で自動追記される -->
<!-- 20件を超えたら統合・整理すること -->
