# 配布ファイルの検査

確認日: 2026-09-16

- Free版 `SKILL.md`: skill-creator の `quick_validate.py` で `Skill is valid!`。
- 元リポジトリの7ファイル: 起点コミットとの差分なし。
- Free版のUIメタデータ: `agents/openai.yaml` をYAMLとして読み込み、スキル名を含む起動例と自動選択設定を確認。
- Markdownのローカル相対リンク: リンク先ファイルの存在を確認。
- 配布ファイル: 個人ユーザー名、今回の私有素材名・保存先、認証トークン形式、メディア・モデル・プロジェクトファイルの混入を検査。
- READMEの導入用PowerShell: 構文解析を実施。別PCでの導入テストは未実施。

これらは配布構造・文書の検査です。GUI編集の実行テストは [TESTING.md](TESTING.md) に記載された範囲に限られます。GitHub上での公開確認は未実施です。
