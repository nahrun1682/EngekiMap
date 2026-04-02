---
name: docs-search
description: 自動生成されたコードベース文書（関数シグネチャ、API仕様、クラス定義、コメント）を検索するときに使う。ユーザーが docs 検索や API 確認を求めた場合、または実装前に正しいシグネチャ確認が必要な場合に適用。
---

# AI Maestro ドキュメント検索

コードベースの自動生成ドキュメントから、関数シグネチャ、クラス定義、API 仕様、コードコメントを検索する。実装前に正しいパターンを確認する。AI Maestro スイートの一部。

## 前提条件

ローカルで AI Maestro が動作し、ドキュメントがインデックス済みであること。

```bash
# ドキュメント検索ツール導入
git clone https://github.com/23blocks-OS/ai-maestro-plugins.git
cd ai-maestro-plugins && ./install-doc-tools.sh
```

## 基本動作

コード変更を実装する前に、まず docs 検索を実行する:

```
依頼受領 -> docs 検索 -> 実装
```

## コマンド

### 検索
| コマンド | 説明 |
|---------|------|
| `docs-search.sh <query>` | セマンティック検索 |
| `docs-search.sh --keyword <term>` | キーワード一致検索 |
| `docs-find-by-type.sh <type>` | 種別検索（function, class, module） |
| `docs-get.sh <doc-id>` | ドキュメント本文取得 |

### インデックス
| コマンド | 説明 |
|---------|------|
| `docs-index.sh` | インデックス生成/更新 |
| `docs-index.sh --watch` | ファイル変更監視で再インデックス |

## 推奨ワークフロー

1. 問題領域キーワードで `docs-search.sh`
2. 候補から `doc-id` を選択
3. `docs-get.sh` で本文取得
4. 実装へ反映
5. 必要に応じて関連 API も再検索

## よくある失敗

- 実装後に docs を確認する
- キーワード一致のみでセマンティック検索を使わない
- 型/戻り値を確認せずに実装する
- 古いインデックスを使う

## 実運用メモ

- API 変更直後は必ず再インデックス
- 関数名だけでなく責務語（auth, retry, timeout など）でも検索
- 競合実装がある場合、最も最近の文書と実コードを照合して判断
