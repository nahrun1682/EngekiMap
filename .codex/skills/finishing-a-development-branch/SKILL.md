---
name: finishing-a-development-branch
description: 実装完了・全テスト成功後に、統合方法（マージ/PR/保持/破棄）を選ぶために使う
---

# 開発ブランチの完了処理

## 概要

明確な選択肢を提示し、選択されたワークフローを実行して作業を閉じる。

**中核原則:** テスト検証 → 選択肢提示 → 選択実行 → クリーンアップ。

## プロセス

### Step 1: テスト検証
- 選択肢提示前に必ずテスト実行
- 失敗なら停止して修正

### Step 2: ベースブランチ特定
- `main` / `master` との merge-base を確認

### Step 3: 4択提示（固定）
1. ローカルでベースへマージ
2. push して PR 作成
3. ブランチを保持
4. 作業を破棄

### Step 4: 選択実行
- 1: checkout → pull → merge → 再テスト → branch 削除
- 2: push → PR 作成
- 3: 保持を報告（削除しない）
- 4: `discard` 明示確認後に削除

### Step 5: worktree クリーンアップ
- 1/2/4 で必要な場合のみ削除
- 3 は保持

## 危険信号

**Never:**
- テスト失敗のまま進行
- 確認なしで破棄
- 明示要求なし force-push

**Always:**
- 選択肢提示前に検証
- 4択を正確提示
- 破棄時は typed confirmation

## 連携

- subagent-driven-development / executing-plans の最終処理で使用
- using-git-worktrees で作った環境の後片付けと連携
