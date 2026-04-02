---
name: using-git-worktrees
description: 現在ワークスペースから分離して機能開発を始めるとき、または実装計画実行前に使う
---

# Git Worktree の使い方

## 概要

Git worktree は同一リポジトリを共有しつつ分離ワークスペースを作り、ブランチ切替なしで並行作業を可能にする。

**中核原則:** 体系的なディレクトリ選定 + 安全確認 = 信頼できる分離。

## ディレクトリ選定

優先順:
1. 既存 `.worktrees` / `worktrees` を使う（両方なら `.worktrees`）
2. CLAUDE.md の指示があれば従う
3. どちらもなければユーザーに確認

## 安全確認

プロジェクトローカルに作る場合:
- `git check-ignore` で ignore されているか確認
- ignore されていなければ `.gitignore` 修正してから作成

グローバルディレクトリ（`~/.config/...`）なら ignore 確認不要。

## 作成手順

1. プロジェクト名を取得
2. 目標パス決定
3. `git worktree add <path> -b <branch>`
4. 言語/ツールを自動判定してセットアップ
5. baseline テスト実行
6. 準備完了をパス付きで報告

## 危険信号

**Never:**
- ignore 未確認で project-local worktree 作成
- baseline テスト省略
- テスト失敗のまま無断進行
- 曖昧状態で場所を決め打ち

**Always:**
- 優先順（既存 > CLAUDE.md > 質問）を守る
- project-local では ignore を確認
- セットアップを自動判定
- clean baseline を確認

## 連携

- brainstorming / subagent-driven-development / executing-plans の開始前に必須
- finishing-a-development-branch で cleanup と連携
