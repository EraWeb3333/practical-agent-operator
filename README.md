# practical-agent-operator

`practical-agent-operator` は、Claude / Codex / ChatGPT 系などのコーディング・ドキュメント作業エージェントに読み込ませる**実務オペレーション規約スキル**です。`SKILL.md` 一枚で、エージェントが「触る前に実ファイルを読む」「変更範囲を限定する」「検証してから完了と言う」「捏造しない」「固定形式で報告する」ように挙動を矯正します。

派生元:

- Source: `elder-plinius/CL4R1T4S` / `ANTHROPIC/CLAUDE-FABLE-5.md`
- URL: https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/CLAUDE-FABLE-5.md
- License: GNU AGPL v3.0（派生物である本リポジトリも同ライセンス）

## このSkillの目的

汎用的な「丁寧にやりましょう」ではなく、**実際にエージェントの出力が変わるレベルの具体的な手順・判断基準・禁止事項・報告形式**を与えることが目的です。具体的には:

- リポジトリを触る前に読むファイルの順番（README → LICENSE → NOTICE → AGENTS/CLAUDE/CONTRIBUTING → manifest → lockfile → CI → tests → src → git status）
- 依頼を 8 つの作業モードに分類し、各モードで「最初に確認すること / やること / やらないこと / 報告に含めること」を固定
- 9 段階の検証ラダー（static → syntax → type → unit → integration → build → lint → smoke → manual）と「実行した／していない／理由」の明示
- 固定の最終報告フォーマット（Changed Files / What Changed / Verification / Risks / Next Action）
- 反ハルシネーション規則（読んでいないファイル・実行していないテスト・存在未確認のパスを口にしない）
- 防御限定のセキュリティレビュー手順と発見報告フォーマット

## 元 CL4R1T4S との差分

本リポジトリは元プロンプトの**全文転載ではありません**。元ソースは特定モデル（Claude Fable 5）のシステムプロンプトであり、人格設定・製品情報・ベンダー固有の内部仕様・実行環境固有のパスなどモデル/プラットフォーム依存の要素を多く含みます。本スキルはそこから**移植可能な運用構造だけ**を抽出し、ベンダー非依存の実務スキルとして再設計しています。

### 抽出した要素（再設計して採用）

- ファイル作成・コード実行の前に必ず関連ファイルを読む「read-first」規律
- ツール利用の節度（最小限の操作・ツール結果に基づいて応答・捏造禁止）
- 成果物の扱い（実ファイルを作る・適切なパスに置く・共有前に検証）
- 検証と報告（何を変更し、何を検証し、何を検証していないかを明示）
- 出典に基づく調査（一次情報優先・出典に確信がなければ含めない・帰属を捏造しない）
- 反ハルシネーション規則

### 除外した要素（公開・移植スキルに不適）

- モデルのアイデンティティ・人格・口調設定
- ベンダー固有の内部仕様・隠しツール・私的 API
- UI 固有の挙動（特定 UI でのレンダリング前提など）
- 安全性回避・ポリシーバイパスにつながる記述
- 古くなり得るプラットフォーム上の断定（モデル名・リリース情報・知識カットオフ日付など）
- 特定モデルの模倣・なりすまし

抽出・除外の詳細は [`NOTICE`](NOTICE) を参照してください。

## 使い方

### Claude / Claude Code

`SKILL.md` をスキルまたはプロジェクト指示として読み込ませます。実作業の前に参照させることで、調査 → 変更 → 検証 → 報告の流れが安定します。

### Codex / ChatGPT 系エージェント

`SKILL.md` をプロジェクト指示（AGENTS.md 等）やシステム/開発者メッセージとして渡します。ベンダー固有の評価ロジックは含まないため、通常のコード作業・調査・ドキュメント作成にそのまま使えます。

### 推奨プロンプト

```text
Use the practical-agent-operator skill in this repository.
Follow its operating principles, task-mode protocol, verification ladder,
reporting format, and anti-hallucination rules.
```

```text
このリポジトリの practical-agent-operator スキルを適用してください。
作業前に実ファイルを読み、変更範囲を限定し、検証ラダーに従い、
最後に固定フォーマットで報告してください。
```

## 推奨ユースケース

- 既存リポジトリの調査・監査（構成、依存、ライセンス、ハイジーン）
- バグ修正・小規模パッチ（最小差分・回帰確認込み）
- ドキュメント／README の実態整合化
- HTML / SVG / Markdown / JSON / YAML / スクリプトなどの成果物生成
- 一次情報に基づく技術調査
- 防御目的のセキュリティレビュー（発見の構造化報告）
- ベンチマーク/評価のスキャフォールド準備

## 非推奨ユースケース

- 安全ガードレールの回避・ポリシーバイパス
- 特定モデル/製品/組織へのなりすまし
- ベンダー内部プロンプトの模倣・再現
- 未検証情報を事実として断定する用途
- 依頼範囲を超えた大規模改変や無断のリファクタ

## ライセンス注意

本リポジトリは [AGPL-3.0](LICENSE) です。AGPL の継承条件により、本スキルを改変・再配布する場合も AGPL v3 を維持し、`LICENSE` を同梱し、改変箇所と日付を `NOTICE` に明記してください。派生元 `elder-plinius/CL4R1T4S` も AGPL-3.0 です。

> This project is based on CL4R1T4S by elder-plinius.
> Modified by EraWeb3Systems on 2026-06-14.
> This modified version is distributed under the GNU Affero General Public License v3.
