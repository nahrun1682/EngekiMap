---
name: subagent-driven-development
description: 現在セッションで、独立タスクを含む実装計画を実行するときに使う
---

# サブエージェント駆動開発

各タスクごとに新しいサブエージェントを起動し、毎タスク後に2段階レビュー（仕様適合 → コード品質）を行う。

**中核原則:** fresh subagent + 2段階レビュー = 高品質で高速な反復。

## 使う条件

- 実装計画がある
- タスクの大半が独立している
- 同一セッションで進めたい

別セッションで進めるなら executing-plans を使う。

## プロセス

1. 計画を読み、全タスク全文を抽出し TodoWrite 作成
2. タスクごとに implementer サブエージェント起動
3. 質問が来たら回答して文脈補足
4. 実装・テスト・自己レビュー
5. spec reviewer で仕様適合確認
6. 不適合なら implementer が修正し再レビュー
7. code-quality reviewer で品質確認
8. 指摘があれば修正→再レビュー
9. TodoWrite 完了更新
10. 全タスク後に最終レビュー
11. finishing-a-development-branch で終了処理

## 危険信号

**Never:**
- main/master で同意なし実装開始
- 仕様/品質レビューどちらか省略
- 未解決 issue を残して次へ進む
- 実装サブエージェントを複数並列で走らせる
- サブエージェントの質問を無視

## 連携

- using-git-worktrees（開始前必須）
- writing-plans（入力計画作成）
- requesting-code-review（レビュー運用）
- finishing-a-development-branch（終了）
- subagent 側は test-driven-development を適用
