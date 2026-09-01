# minecraft-remote-protocol

Minecraft Remote Protocol移管候補として作成され、現在park中の公開bootstrap repositoryです。現行ownerではありません。

## McRemote SSOT

McRemote固有の設計判断の正本はGitHub上の`Naohiro2g/mc-remote-knowledge`です。

McRemote固有文脈に依存する作業に入る前に、agentはそのSSOT repositoryの関連文書を必ず読んでください。対象には
architecture、protocol、deployment、contributor workflow、learning design、およびMcRemote固有の判断理由に依存する
挙動変更が含まれます。

最初に、knowledge repositoryのremote `main`から最新のdev agent runtime protocolだけを取得して指示として読んでください。
取得元file全体を会話へ出力してはいけません。

```bash
protocol_source="$(mktemp)"
knowledge_commit="$(gh api repos/Naohiro2g/mc-remote-knowledge/commits/main -q .sha)"
gh api "repos/Naohiro2g/mc-remote-knowledge/contents/00-hub/dev-repo-protocol_ja.md?ref=$knowledge_commit" \
  -q .content | base64 -d > "$protocol_source"
if [ "$(grep -Fxc '<!-- BEGIN: DEV-AGENT-RUNTIME -->' "$protocol_source")" -ne 1 ] || \
   [ "$(grep -Fxc '<!-- END: DEV-AGENT-RUNTIME -->' "$protocol_source")" -ne 1 ]; then
  echo "dev agent runtime marker missing or duplicated" >&2
  exit 1
fi
printf 'knowledge commit: %s\n' "$knowledge_commit"
awk '/^<!-- BEGIN: DEV-AGENT-RUNTIME -->$/{reading=1;next} \
     /^<!-- END: DEV-AGENT-RUNTIME -->$/{reading=0} \
     reading' "$protocol_source"
```

SSOT repositoryへアクセスできない場合は作業を止め、その旨を明示してください。このrepository単体、assistant memory、
過去会話、local推論から欠けた文脈を補完してはいけません。

このfileはSSOTを複製しません。複製はdriftを生みます。

- 関連spoke: `10-protocol/`

## Repository固有の指示

- park中はcontract、fixture、package、tooling、consumer参照を変更しません。
- 現行のexecutable projection／shared fixture ownerは`Naohiro2g/scratch-editor:mc-remote/protocol`です。
- 本repositoryからsuccessor fixture、package、releaseを発行せず、b7 release inputとして扱いません。
- post-b7の人間レビューでProtocol、conformance、WireScope、Bridge、TCP／browser接続を一体評価するまで移管作業を再開しません。
- consumer固有実装、Scratch block、McRemote handler、Python／Java Client APIを本repositoryへ移しません。
- packageは別途批准されるまでprivateのままにし、npmへpublishしません。
- secret、private endpoint、credential、UUIDの実値をsource、fixture、logへ残しません。
