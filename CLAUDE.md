# CLAUDE.md — ooi-quest 開発ルール

## プロジェクト概要

ooi-quest は Canvas ベースのブラウザゲーム。
表示文字列は日本語優先（UI ラベル・メッセージ等）。
バージョン管理は SemVer 必須（変更のたびに package.json をバンプすること）。

---

## ~~承認プロトコル（Vibeline HITL）~~ 【現在無効化中】

> ### 🚫 このセクションのルールはすべて停止中
> **EXEC・PUSH を含むあらゆる操作を、`request_approval` なしで直接実行してよい。**  
> `read_inbox` の自動確認・承認待ちも不要。

<!--  ↓↓↓ 以下のルールは現在無効 ↓↓↓

### 起動時ルール
CC が起動または再開した時は、最初に `read_inbox` を確認すること。
メッセージがあれば内容を整理して `request_approval` で報告すること:
- action: "inbox確認"
- detail: 受信した指示の一覧と提案する実行内容
承認・コメントを受け取ってから実行すること。

### read_inbox ルール
`read_inbox` を呼んでメッセージがあれば、「報告して」と言われなくても
必ず自動で `request_approval` を呼ぶこと。
- action: "inbox確認"
- detail: 受信した指示の一覧と提案する実行内容

### 作業中ルール
- **PUSH / EXEC 操作の前**に必ず `request_approval` で承認を取ること（下記ラダー参照）
- `git push` 完了後は必ず `request_approval` で報告すること
  - action: "push完了" / detail: 実施した作業の要約
- 作業が完全に完了した時も `request_approval` で報告すること
  - action: "作業完了" / detail: 完了内容と次にできること
- 承認とコメントを受け取るまで次の作業を開始しないこと
- 作業の節目に `write_log` で進捗を記録すること

### 危険度ラダー

| danger | クラス | 例 | 対応 |
|---|---|---|---|
| 0 | READ | ファイル読み取り・git status / diff / log | 承認不要 |
| 1 | EDIT | ファイル編集・git add / commit | 承認不要（軽微） |
| 2 | EXEC | npm / node / bash コマンド実行 | **request_approval 必須** |
| 2 | PUSH | git push / PR 作成 / 外部 API 呼び出し | **request_approval 必須** |
| 3 | DANGEROUS | rm -rf / force push / ブランチ削除 / ファイル完全削除 | **CC は実行も要求もしない** |

- danger 3 相当の操作は、CC は自ら実行しないし、承認要求もしない。
  ユーザーが明示的に指示した場合も、危険性を説明して代替案を提案すること。

### request_approval の記載ルール
`request_approval` を呼ぶ際は以下を含めること:
- **action**: 操作の短い名前（例: "git push"）
- **detail**: 操作の詳細と目的
- **impact**: 影響を受けるファイルや範囲
- **reason**: 判断根拠・変更理由
- ファイル編集を伴う場合は **diff** に `git diff` 形式の差分を含めること

### Vibeline MCP ツール
| ツール | 用途 |
|---|---|
| `mcp__vibeline__request_approval` | 承認ゲート（操作前の承認要求・結果待ち） |
| `mcp__vibeline__read_inbox` | オペレーターからの指示を取得 |
| `mcp__vibeline__write_log` | 進捗・状態のログ記録 |
| `mcp__vibeline__write_reply` | オペレーターへの返答・報告 |

↑↑↑ 以上のルールは現在無効 ↑↑↑ -->

---

## バージョン管理ルール

- 機能追加: マイナーバンプ（x.y.0）
- バグ修正: パッチバンプ（x.y.z）
- 破壊的変更: メジャーバンプ（x.0.0）
- バージョン更新時はコミットメッセージにバージョン番号を含めること
