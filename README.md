# AI Driven Development Template (v2.1)

AIエージェント（Claude Code）との協働を前提に最適化された、Next.js/TypeScript開発用テンプレートです。
「コンテキストの維持」「自律的なエラー対応」「明確な責任分担」を設計思想としています。

## 特徴

- **Linear駆動開発**: チケットの状態を正（Source of Truth）とし、AIの記憶喪失を防ぐ `suspend` / `resume` フロー。
- **Spec駆動設計**: `cowork` で作成したMarkdown仕様書を元に、`architect` が実装計画を立案。
- **自律的品質管理**: CI失敗を検知してチケット化する `handle-ci-failure` や、脆弱性を監査する `security-reviewer`。
- **トークン効率**: 不要なファイルを読ませない `.claudeignore` と、役割に応じたモデル（Haiku/Opus）の使い分け。

## 前提条件 (Prerequisites)

1. **Linear MCP Server**:
   - このテンプレートは Linear との連携を前提としています。
   - `suspend`, `resume`, `ticket-feedback`, `handle-ci-failure` コマンドに必要です。
   ```bash
   claude mcp add linear-server https://mcp.linear.app/sse
   ```

2. **GitHub CLI (`gh`)**:
   - PR作成やCIログの確認に使用します。

## ディレクトリ構成

```
.claude/
├── commands/           # 人間が実行するマクロ (yolo, suspend, resume, plan...)
├── skills/             # AIが判断して使うツール (review, commit, ci-handler...)
├── agents/             # 専門家のペルソナ (architect, security-reviewer...)
└── rules/              # ガードレール (security, style, testing)
docs/
└── specs/              # 仕様書置き場 (Source of Truth for Plan)
```

## ワークフロー

### 1. 計画フェーズ (Architect)

1. 人間または `cowork` で仕様を策定し、`docs/specs/feature-x.md` に保存。
2. 設計コマンドを実行:
   ```bash
   claude plan docs/specs/feature-x.md
   ```
3. AI (Architect) が実装計画を提示し、Linearのタスク候補を作成。

### 2. 実装フェーズ (Coder)

1. タスクを開始:
   ```bash
   claude resume
   ```
2. 実装完了後、自動でPR作成:
   ```bash
   claude commit-push-pr-flow
   ```

### 3. レビュー・品質フェーズ (Reviewer)

- **PR作成後**: 自動でCIが実行されます。
- **CI失敗時**: 通知が来たら以下を実行（待機する必要はありません）:
  ```bash
  claude handle-ci-failure
  ```
- **コードレビュー**:
  ```bash
  claude review-flow --deep
  ```
  ※ `security-reviewer` が脆弱性を検知した場合、マージ阻止を勧告します。

### 4. 中断・終了 (Suspend)

作業を中断する場合、コンテキストをLinearに保存して終了します。

```bash
claude suspend
```
