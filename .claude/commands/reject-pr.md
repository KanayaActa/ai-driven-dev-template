---
name: reject-pr
description: 重大な欠陥によりPRを却下し、タスクを巻き戻します
model: haiku
---

現在のPRをクローズし、出直しを図ります。

## 手順

1. **理由の確認**: ユーザーに却下理由を確認（セキュリティ問題、設計ミス等）

2. **PRクローズ**:
   ```bash
   gh pr close --comment "Closing due to: [理由]"
   ```

3. **Linearのタスク状況を確認**:
   - 「タスクを In Progress に戻しますか？」
   - 「別の Bug チケットを作成しますか？」
   - Security Issue の場合は Priority: Urgent を提案

4. **ローカルのブランチ整理**:
   ```bash
   git checkout main
   git pull
   ```
   - 修正用ブランチを新たに作成するか確認
   - 例: `fix/security-patch-...`

5. **完了報告**: 「PRをクローズしました。Linearの状態を [状態] に更新しました。」

## 意図
汚れたコミット履歴をマージせず、クリーンな状態で再実装を始めるため。
