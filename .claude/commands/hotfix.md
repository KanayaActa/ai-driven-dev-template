---
name: hotfix
description: 緊急のバグ・脆弱性修正用ブランチを作成します
model: haiku
---

緊急修正モードを開始します。

## 手順

1. **最新化**:
   ```bash
   git checkout main
   git pull
   ```

2. **Hotfixブランチ作成**:
   ```bash
   git checkout -b hotfix/<issue-description>
   ```

3. **Linearチケット作成を促す**:
   - `Bug` タイプのチケットを作成
   - Priority: `Urgent` に設定
   - 必要に応じてMCPで作成支援

4. **修正ガイダンス**:
   - テストは最低限の再現テストとリグレッションテストに絞る
   - 完了後は以下を実行：
     ```bash
     gh pr create --base main --label "hotfix"
     ```

5. **完了後**: 通常の `commit-push-pr-flow` に合流

## 注意
Hotfixは最小限の変更に留め、根本対策は別チケットで対応すること。
