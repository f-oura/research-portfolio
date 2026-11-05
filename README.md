# Research Portfolio

研究プロジェクトを横断して、目的・優先順位・依存関係・次の判断を扱う個人用の管理リポジトリ。
個別の実装、Task、Evidence、実行環境は Research Project OS 側を正本にする。

## 最初に読む

1. [エージェント規則](AGENTS.md)
2. [研究方針](strategy.md)と[現在の重点](focus.md)
3. [プロジェクト登録簿](projects/registry.yaml)
4. 対象プロジェクトの AGENTS.md、current_state、task_board、最新の有効な判断・handoff

## 最小運用

- プロジェクト追加時: registry に ID、repository、profile の参照を追加する。進捗は転記しない。
- 横断レビュー時: `reviews/_template.md` を日付付きファイルにコピーし、参照 commit と未確認事項を残す。
- 優先順位を決めた時: `decisions/_template.md` から記録し、focus にリンクする。提案と承認を区別する。
- 個別作業へ移る時: 対象 Project OS で Task と必要な Context Pack を用意する。
- 作業後: 結果は個別プロジェクトに記録し、全体の判断が変わる場合だけ portfolio を更新する。

[接続方法と確認した上流版](docs/project-os-integration.md)を参照。
このリポジトリ自体を個別研究用 bootstrap に通す必要はない。Portfolio は Project OS の検証対象スキーマではない。

## ファイルの役割

- `strategy.md`: 長期の問いと選択基準。
- `focus.md`: 今の重点と再検討条件。
- `projects/registry.yaml`: プロジェクト正本の参照先。
- `relations.yaml`: 成果の受け渡しと依存関係。個別 Task の依存は元プロジェクトに置く。
- `inbox.md`: 未整理のアイデア。
- `decisions/`, `reviews/`: 判断と日付付きの観測履歴。
- `generated/`: 必要時に作る派生物。Git 対象外。

`highp-program` を実験単位の管理入口として登録済み。
そのmember registryに `e88daq-dev`、`highp-ana-dev`、`highp-online-ana-dev`、`amaneq-receiver` を登録している。
従来のamaneq-receiverの接続情報はhighp-programへ移管し、安定IDと既存profileを保持した。
研究の優先順位・予算・期限は未設定。

program登録はProject OSの個別projectとは異なる。registryの `checkout_hint` はこのrepo root基準、
`member_registry` は参照先programのroot基準で解決する。そこで対象projectを選び、その規則と正本を読む。
この階層は所属を表し、`relations.yaml` の技術的依存とは別。最上位がすべての子の進捗を複製する必要はない。
共有前に、参照先の共同研究の共有範囲を確認する。
