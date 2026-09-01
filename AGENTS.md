# minecraft-remote-protocol

Minecraft Remote Protocolの実行可能投影とshared conformance fixtureを所有する公開repositoryです。

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

- 本repositoryはhuman-readable Protocol SSOTではなく、批准済みcontractのexecutable projection／fixture ownerです。
- wireの意味、method、reason、versionを独自判断で追加・変更しません。必要ならknowledgeの人間レビューへ戻します。
- fixture変更ではowner commit、path、bytes、SHA-256、case ID ledger、predecessorからのsemantic diffを返します。
- consumer固有実装、Scratch block、McRemote handler、Python／Java Client APIを本repositoryへ移しません。
- packageは別途批准されるまでprivateのままにし、npmへpublishしません。
- secret、private endpoint、credential、UUIDの実値をsource、fixture、logへ残しません。
