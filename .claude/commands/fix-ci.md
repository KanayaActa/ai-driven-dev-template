---
name: fix-ci
description: CI (GitHub Actions) の失敗を分析し、ローカルで修正・検証してPushします
model: opus
---

CIの失敗ログを解析し、修正を行います。

## 前提
- このプロジェクトは `pnpm` を使用しています。
- CIの設定は `.github/workflows/ci.yml` にあります。

## 手順

1. **状況確認**:
   - `gh run list --limit 1 --json status,conclusion,workflowName` を実行。
   - `conclusion` が `failure` でなければ、「CIは失敗していません」と報告して終了。

2. **ログ取得と分析**:
   - `gh run view --log-failed` を実行。
   - エラーの種類を特定する：
     - **Lint Error**: `eslint` / `prettier` 関連
     - **Type Error**: `tsc` 関連
     - **Test Failure**: `vitest` 関連
     - **Build Error**: ビルドプロセス関連

3. **修正サイクル**:
   - エラー原因のコードを修正。
   - **重要**: 修正後は必ずローカルで対応するコマンドを実行して検証すること。
     - Lint系: `pnpm lint`
     - Type系: `pnpm type-check`
     - Test系: `pnpm test`

4. **反映**:
   - 検証が通ったらコミットとPushを行う。
   - `git add .`
   - `git commit -m "fix(ci): resolve [エラーの種類] errors"`
   - `git push`

5. **完了**:
   - 「修正をPushしました。CIの再実行を見守ります。」と報告。
