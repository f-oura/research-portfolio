# Research Project OS との接続

## 確認した版

2026-10-31 (Asia/Tokyo)、GitHub の main を確認した。
確認 revision: `97062125c64005a85f5f70ecb5cf358279408c3c`。
ローカル checkout は読み取りが完了しなかったため、現在のローカル内容や dirty 状態との同一性は未確認。

[README](https://github.com/f-oura/research-project-os/blob/97062125c64005a85f5f70ecb5cf358279408c3c/README.md)、
[SKILL](https://github.com/f-oura/research-project-os/blob/97062125c64005a85f5f70ecb5cf358279408c3c/SKILL.md)、
[record schema](https://github.com/f-oura/research-project-os/blob/97062125c64005a85f5f70ecb5cf358279408c3c/references/project-schema.md)、
[philosophy](https://github.com/f-oura/research-project-os/blob/97062125c64005a85f5f70ecb5cf358279408c3c/references/philosophy.md)
を基準にした。

上流は scripts / templates / profiles / references を持ち、個別 project の Task・Evidence・Decision・Execution を管理する。
Portfolio の優先順位・予算判断は上流の明示的な scope 外なので、ここで薄く補う。
上流コードやスキーマを複製せず、profile と既存 CLI を参照する。

## 正本の分担

| 内容 | 正本 |
|---|---|
| 研究全体の重点・横断判断 | この repo の focus / decisions |
| 個別研究の問い・現状・Task・Evidence | 個別 project |
| canonical role と実ファイルの対応 | Project OS profile |
| project への接続先 | projects/registry.yaml |
| 実行 host と環境 | 個別 project の environments / executions |
| 横断レビュー | この repo の reviews（日付付き snapshot） |

native project では標準の `docs/project/current-state.yaml` と `docs/project/task-board.yaml` を読む。
mapped project は指定 profile の `canonical` を読む。役割名は `current_state` / `task_board` / `agent_policy` 等。
amaneq-receiver は上流の `profiles/amaneq-receiver.yaml` を使用する。
profile の `charter: README.md` なども上流の mapping を尊重し、古い導入計画から推定して変更しない。

## CLI の使用例

以下は portfolio root から実行する。実行前に OS checkout の HEAD が確認版と一致し、変更がないことを確認する。
異なる版なら差分をレビューして registry の reviewed_revision を更新する。ユーザーの checkout を自動 reset しない。

```bash
OS_ROOT="../skills/research-project-os"
PROJECT_ROOT="../jparc-saphire/daq/amaneq-receiver"
PROFILE="$OS_ROOT/profiles/amaneq-receiver.yaml"
git -C "$OS_ROOT" rev-parse HEAD
git -C "$OS_ROOT" status --short
python3 "$OS_ROOT/scripts/audit_project.py" "$PROJECT_ROOT" --profile "$PROFILE"
python3 "$OS_ROOT/scripts/validate_project.py" "$PROJECT_ROOT" --profile "$PROFILE"
```

上記は対象 project の監査・検証。portfolio に validate_project を実行しない。
監査の warning は記録する。自動的な移行・依存の導入・project の修正は行わない。

実際の Task ID を task board から選んだ後、必要な場合にだけ Context Pack を作る:

```bash
TASK_ID="REPLACE_WITH_EXISTING_TASK_ID"
python3 "$OS_ROOT/scripts/context_pack.py" "$PROJECT_ROOT" \
  --profile "$PROFILE" --task "$TASK_ID" \
  --purpose "選択した Task の次の判断を確認する"
```

native project では `--profile` を省略する。未知の Task ID は上流で失敗する。
Pack は標準出力へ出る。保存が必要なら共有範囲を確認して `generated/` に保存し、正本として commit しない。
今回の作成では個別 project の audit / validate / Context Pack 生成は未実行。現状や hardware の検証を主張しない。

## 拡張するタイミング

プロジェクト登録と横断レビューを実際に使い、参照切れや転記負担が繰り返し問題になる場合に、read-only の集約・検証ツールを追加する。
自動同期や agent の常駐実行はこの最小構成には含めない。
