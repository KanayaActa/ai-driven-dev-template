---
name: init-plus
description: CLAUDE.mdを生成
model: opus
disable-model-invocation: true
---

create CLAUDE.md that memory current project.

Include:
- common bash commands
- code style conventions (reference .prettierrc, .eslintrc.json)
- ui and content design guidelines
- how to do state management, logging, error handling, gating, and debugging
- pull request template
- Linear project prefix
- 「過去の学習」セクション（空で作成、20件超えたら統合する旨を記載）
