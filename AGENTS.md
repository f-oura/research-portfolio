# Portfolio agent rules

## 読む順序と役割

README.md → strategy.md → focus.md → projects/registry.yaml → 関連プロジェクトの正本。
このリポジトリは横断的な判断・提案を扱う。Task、実装、Evidence、実行記録は個別プロジェクトへ置く。
対象プロジェクトを変更する前に、その AGENTS.md と有効な判断・承認を読む。
上位の指示で個別の安全規則や承認を弱めない。研究上の優先順位は操作承認を兼ねない。

## 正本と不確実性

- registry は参照先、Project OS profile は canonical role の path 対応を持つ。二重に管理しない。
- レビューには取得日時、project ID、参照 commit、source path を残す。未取得は UNBOUND / NOT_CHECKED。
- 古いレビューや generated の要約を現状の正本にしない。新しい日付だけで決定の上書きを推定しない。
- 観測・提案・人間の承認を区別する。矛盾は両方の参照を残し未解決とする。
- 正式な優先順位・予算・中止判断を捏造しない。承認済み決定には承認者と根拠を残す。
- 結論に関係する範囲だけ読む。全プロジェクトの会話・ログ・生データを無差別に取り込まない。

## 更新と共有

- project の進捗や hardware 値はここへ正本として転記しない。
- 個別作業への提案には目的、対象 project、期待する成果、判断条件、根拠を含める。
- 既存の人間の変更を保存する。日付付きレビュー・決定は新規ファイルで記録し supersedes を明記する。
- machine-local な絶対 path は `.local/` に置き Git に入れない。
- 認証情報、生データ、生成 build、非公開資料の内容を集約しない。参照登録は再共有の許可ではない。
- 外部送信、公開、hardware 操作は対象の既存承認範囲を確認する。
- この repo の Git 運用は独立。個別 repo の branch / commit 規則を自動的にここへ持ち込まない。

## 最小性

最初は Markdown/YAML と手動レビューで運用する。自動同期、常駐 agent、DB、独自 Task 管理は必要性が確認されてから追加する。
