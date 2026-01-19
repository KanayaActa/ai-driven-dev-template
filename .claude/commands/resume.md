---
name: resume
description: Linearのタスクから作業を再開します（current-prの上位互換）
model: haiku
---

Linearの情報を正として作業環境を復元します。

## 手順

1. **タスク取得**: Linearから `State: In Progress` の自分のタスク一覧を取得し、ユーザーに選択させる。
   - タスクがない場合は `gh pr list --author @me` でPR一覧を表示

2. **コンテキスト復元**: 選択されたタスクの以下を読み込む：
   - 最新のコメント（中断メモ）
   - Description
   - サブタスク一覧

3. **環境復元**:
   - メモに記載されたブランチを `git checkout`
   - `git pull` で最新化
   - PRがある場合は `gh pr diff` で変更内容を確認

4. **mainブランチとの乖離確認（重要）**:
   ```bash
   git fetch origin main
   git log --oneline HEAD..origin/main | head -10
   ```
   - 差分がある場合は「⚠️ main に [N件] の新しいコミットがあります」と警告
   - コンフリクトリスクがある場合は `git rebase origin/main` または `git merge origin/main` を提案

5. **CLAUDE.md読み込み**: `cat CLAUDE.md` でプロジェクトルールを再確認

6. **再開案内**: 以下の形式で要約して待機：

「現在は [ブランチ名] で [タスク名] を進めています。
前回の中断メモ: [内容要約]
main との差分: [N件のコミット / なし]
次にやるべきこと: [Next Action]
ここから再開しますか？」
