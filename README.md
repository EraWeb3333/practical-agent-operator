# practical-agent-operator

`practical-agent-operator` は、Claude / Codex / Claude Code / Codex系エージェントで使うためのスキルです。

対象ソースは以下です。

- Source: `elder-plinius/CL4R1T4S` / `ANTHROPIC/CLAUDE-FABLE-5.md`
- URL: `https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/CLAUDE-FABLE-5.md`
- Purpose: ソースの行動パターンをエージェント向けの運用スキルとして整理する

## Directory layout

```text
├─ SKILL.md
├─ README.md
└─ LICENSE
```

## What this skill does

このスキルは、対象ソースに含まれる行動パターンを、公開リポジトリ向けの `SKILL.md` として整理したものです。

主な用途は以下です。

- リポジトリ調査
- コード修正
- バグ調査
- ドキュメント作成
- GitHub作業
- ツール利用を前提とした作業
- 生成物の作成と検証
- 事実確認が必要な調査

## What this skill is not

このスキルは以下を目的にしていません。

- jailbreak / guardrail bypass
- 特定モデルへのなりすまし
- Anthropic / OpenAI の公式プロンプト再配布
- 安全ポリシーを弱めるための指示

## Design policy

`SKILL.md` は、対象ソースをスキルとして使いやすい形に整理しています。

特に以下を重視しています。

- 実ファイル・実リポジトリを確認してから作業する
- 余計なリファクタや仕様変更をしない
- 小さく安全な差分を作る
- 検証できるものは検証する
- 事実と推測を分ける
- 最新情報が必要な場合は一次情報を確認する
- 出力ファイル・変更ファイル・未検証事項を明示する
- 危険用途や不正用途には転用しない

## Usage

### Claude / Claude Code style

`SKILL.md` をスキルとして読み込ませます。このスキルを参照させることで、リポジトリ調査、ファイル生成、コード修正、検証、報告の流れを安定させます。

### Codex style

Codex側では、`SKILL.md` をプロジェクト指示またはエージェント向け運用指示として参照させます。通常のコード作業・調査作業・ドキュメント作成にそのまま使えます。

## Recommended prompt

```text
Use the practical-agent-operator skill in this repository.
Follow its operating loop, repository behavior, factuality rules, and safety boundaries.
```

日本語で使う場合は以下で十分です。

```text
このリポジトリの practical-agent-operator スキルを使用してください。
```

## License

このリポジトリは [AGPL-3.0](LICENSE) でライセンスされています。

対象ソース (`elder-plinius/CL4R1T4S`) も AGPL-3.0 でライセンスされています。このリポジトリは対象ソースをそのまま転載するのではなく、行動パターンをスキルとして再構成したものです。

This project is based on CL4R1T4S by elder-plinius.
Modified by EraWeb3Systems on 2026-06-14.
This modified version is distributed under the GNU Affero General Public License v3.

