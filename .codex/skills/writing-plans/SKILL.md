---
name: writing-plans
description: 仕様や要件があり、複数ステップ作業をコード着手前に計画化するときに使う
---

# 計画を書く

## 概要

実装者がコードベース文脈をほぼ知らない前提で、包括的な実装計画を書く。各タスクで触るファイル、必要コード、テスト、参照ドキュメント、検証方法まで具体化する。計画は小さなタスクへ分解する。DRY、YAGNI、TDD、頻繁コミット。

**開始時に宣言:** "I'm using the writing-plans skill to create the implementation plan."

**文脈:** 専用 worktree（brainstorming で作成）で実施。

**保存先:** `docs/plans/YYYY-MM-DD-<feature-name>.md`

## タスク粒度

**1ステップ=1アクション（2〜5分）:**
- 失敗テストを書く
- 失敗を確認する
- 最小実装を書く
- 成功を確認する
- コミットする

## 計画ドキュメントヘッダー

**全計画は次で開始:**

```markdown
# [Feature Name] Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

---
```

## タスク構造

```markdown
### Task N: [Component Name]

**Files:**
- Create: `exact/path/to/file.py`
- Modify: `exact/path/to/existing.py:123-145`
- Test: `tests/exact/path/to/test.py`

**Step 1: Write the failing test**
...
```

## 覚えること
- ファイルパスは常に正確
- 抽象指示でなく具体コードを書く
- コマンドは期待結果つき
- 関連スキルは `@` で参照
- DRY, YAGNI, TDD, 頻繁コミット

## 実行引き渡し

保存後に次を提示:

1. **Subagent-Driven（同セッション）** - タスクごとに新規サブエージェント、タスク間レビュー
2. **Parallel Session（別セッション）** - executing-plans でバッチ実行

**Subagent-Driven 選択時:**
- **REQUIRED SUB-SKILL:** superpowers:subagent-driven-development

**Parallel Session 選択時:**
- 新セッションで **superpowers:executing-plans** を使用
