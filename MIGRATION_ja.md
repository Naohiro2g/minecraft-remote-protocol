# protocol owner移管記録

## 移管元

- repository: `Naohiro2g/scratch-editor`
- source commit: `607cda40588ec4579c503d457c3784385419ac65`
- source path: `mc-remote/protocol`
- original introduction: `48fdac6e0ef7ea162bf796a9b9eea26a2d07c786`
- imported scope: tracked package source、設定、test、共有fixture

本repositoryの初期commitは、上記source commitのsubtree snapshotをrootへ移したものです。元repositoryのcommit historyと
既存tag／release evidenceは書き換えず、過去fixtureのprovenanceとして参照します。

## 所有境界

- 人間可読のProtocol SSOT: `mc-remote-knowledge/10-protocol`
- executable projection／shared fixture owner: 本repository
- consumers: McRemote、Minecraft Remote for Python、Scratch Client、Java Client Library、将来の独立実装
- Scratch固有のblock／VM mirror／Bridge／WireScope: `scratch-editor`

owner移管は、Scratch製品実装の完了を他componentのfixture gateにしないためのものです。knowledgeで批准されていない
wire変更を本repositoryだけで追加しません。

## b7移管境界

初期snapshotの`test/fixtures/direction-lightning-v23.1.json`は旧permission contractのpredecessorです。
`mcr.lightning`削除とhello時の独立した`mcr.online`／`mcr.offline`／build range snapshotを含むsuccessor fixtureは、
本repositoryの専用branchで発行します。移管元fixtureを黙って書き換えた履歴として扱いません。
