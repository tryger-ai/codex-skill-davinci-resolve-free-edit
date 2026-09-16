# DaVinci Resolve Free Edit — Computer Use 実験版

Windows の無料版 DaVinci Resolve を Codex の Computer Use で操作し、編集可能なタイムラインを作成するスキルです。現在の実験版は **0.1.0-preview** です。

Yasei-no-otoko さんの [codex-skill-davinci-resolve-edit](https://github.com/Yasei-no-otoko/codex-skill-davinci-resolve-edit) を起点としています。元版は MCP と画面操作を併用し、この Free 版は Resolve の操作を画面操作に統一します。作者公認や完全互換を意味しません。

> GitHub上の公開フォークです。元リポジトリの利用条件は確認待ちで、一般的な改変・再配布を許諾するライセンスは付与していません。[出典とライセンス状況](PROVENANCE.md)を確認してください。

## インストール対象

**Free 版は `skills/davinci-resolve-free-edit/` だけです。** ルートの `SKILL.md`、`agents/`、`references/`、`scripts/` は元の MCP 版を変更せず残しています。リポジトリ全体やルートのスキルを Free 版としてインストールしないでください。

## 必要環境

- Windows と、起動・操作可能な DaVinci Resolve 無料版。
- ローカルの Windows アプリを操作できる Codex 環境。本検証では Codex Desktop と `computer-use:computer-use` を使用。
- その Computer Use スキルに付属する `node_repl` と `@oai/sky` が実際に呼べること。ブラウザ操作だけの環境では代用できません。
- 素材・保存先へのアクセス権と、使用するフォント。

Computer Use の提供状況は利用環境によって異なります。このリポジトリにプラグイン本体は含まれず、スキルをコピーするだけでは導入されません。`@oai/sky` を任意の npm パッケージとして別途インストールする手順も提供しません。利用中の Codex に対応する Computer Use がない場合、画面編集は実行できません。

文字起こしは任意の追加環境です。支給原稿・SRTがあれば利用でき、音声から作る場合は既存のローカル文字起こし環境が必要です。本検証では faster-whisper のローカルモデルを使用しましたが、モデルは同梱せず、自動取得もしません。音声の自然さを聴き分ける機能は含みません。

「Free」は Resolve 無料版への対応を指します。Codexや周辺サービスの料金・利用条件まで無料とする意味ではありません。

## 手動インストール

このリポジトリを取得したフォルダで PowerShell を開き、以下を実行します。既存スキルがある場合は停止します。更新時は差分を確認してから置き換えてください。

```powershell
$sourceSkill = Join-Path (Get-Location) 'skills\davinci-resolve-free-edit'
$codexBase = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE '.codex' }
$skillParent = Join-Path $codexBase 'skills'
$destinationSkill = Join-Path $skillParent 'davinci-resolve-free-edit'
if (-not (Test-Path -LiteralPath (Join-Path $sourceSkill 'SKILL.md'))) { throw 'リポジトリのルートで実行してください。' }
if (Test-Path -LiteralPath $destinationSkill) { throw '既存スキルがあります。差分を確認して更新してください。' }
New-Item -ItemType Directory -Path $skillParent -Force | Out-Null
Copy-Item -LiteralPath $sourceSkill -Destination $destinationSkill -Recurse
```

導入後は新しいタスクでスキルが認識されることを確認し、最初に次のように依頼してください。

> $davinci-resolve-free-edit を使います。まず Windows の Resolve 画面を読み取れるか確認して、表示されたバージョン・プロジェクト名を報告してください。まだ編集しないでください。

操作できたら、[依頼例](examples/edit-request.md)のように素材、残す範囲、音声の扱い、保存先を指定します。初回は短いテスト素材と独立したタイムラインを使ってください。

## 対応範囲と制限

Text+ の日英テロップ作成、書式設定、保存、MP4書き出しを1環境で確認しました。複数素材の編集、映像・音声の別配置、速度変更、SRT読み込み、フェードは手順を用意していますが、この版での実地検証は未完了です。[検証記録と再現手順](TESTING.md)を参照してください。

- 元の映像や既存タイムラインを保護し、作業用コピーまたは新規タイムラインを使います。
- GUI の表示・キーボード割当・ウィンドウ状態に依存し、大量処理の速度や無人実行の成功率は保証していません。
- Studio専用機能を無料版に追加せず、Resolve MCP・外部スクリプティングAPI・DB直接編集も利用しません。
- 参考作品の完全一致や、利用者の好みの自動学習は保証しません。書式は指定された参考から確認します。
- 音声の文字起こし・波形分析と、直接聴取による品質評価は区別して報告します。

## 更新・不具合報告

修正時は再現条件、期待する動作、実際の動作、確認結果を記録します。Windows/Resolve/Codex/Computer Use の版、UI言語、キーボード設定も添えてください。私有素材・氏名・ローカルの個人パスを含む画像やログは公開しないでください。

変更は [CHANGELOG.md](CHANGELOG.md)、公開前の残作業は [RELEASE-CHECKLIST.md](RELEASE-CHECKLIST.md) に記載しています。
