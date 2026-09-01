# Protocol移管候補bootstrap記録

> 状態: park。以下はsnapshot importのprovenanceであり、owner移管完了を示さない。

## 移管元

- repository: `Naohiro2g/scratch-editor`
- source commit: `607cda40588ec4579c503d457c3784385419ac65`
- source path: `mc-remote/protocol`
- original introduction: `48fdac6e0ef7ea162bf796a9b9eea26a2d07c786`
- imported scope: tracked package source、設定、test、共有fixture

本repositoryの初期commitは、上記source commitのsubtree snapshotをrootへ移したものです。元repositoryのcommit historyと
既存tag／release evidenceは書き換えず、過去fixtureのprovenanceとして参照します。

## 現在の所有境界

- 人間可読のProtocol SSOT: `mc-remote-knowledge/10-protocol`
- executable projection／shared fixture owner: `Naohiro2g/scratch-editor:mc-remote/protocol`
- 本repository: 未採用の移管candidate snapshot
- consumers: McRemote、Minecraft Remote for Python、Scratch Client、Java Client Library、将来の独立実装

post-b7の横断reviewではProtocol、conformance、WireScope、Bridge、TCP／browser接続を一体で評価します。共通TypeScript
tooling monorepo案は有力候補ですが、WireScope分離案、hybrid、Bridgeの維持／廃止を含む最終topologyは未決です。

## b7境界

初期snapshotの`test/fixtures/direction-lightning-v23.1.json`は旧permission contractのpredecessorです。
`mcr.lightning`削除とhello時の独立した`mcr.online`／`mcr.offline`／build range snapshotを含むsuccessor fixtureは、現行ownerの
scratch-editorから発行します。本repositoryから発行せず、consumer参照とb7 gateを切り替えません。
