## Network > Security Groups > API v2ガイド

APIを使用するにはAPIエンドポイントとトークンなどが必要です。 [API使用準備](/Compute/Compute/ja/identity-api/)を参考にしてAPIを使用するために必要な情報を準備します。

セキュリティグループAPIは`network`タイプエンドポイントを利用します。正確なエンドポイントはトークン発行レスポンスの`serviceCatalog`を参照します。

| タイプ | リージョン | エンドポイント |
|---|---|---|
| network | 韓国(パンギョ)リージョン<br>韓国(ピョンチョン)リージョン<br>日本リージョン | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://jp1-api-network-infrastructure.nhncloudservice.com |

APIレスポンスにガイドに明示されていないフィールドが現れることがあります。これらのフィールドはNHN Cloud内部用途で使用し、事前の告知なしに変更される場合があるため使用しません。


## セキュリティグループ
### セキュリティグループリスト表示
```
GET /v2.0/security-groups
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するセキュリティグループID |
| tenant_id | Query | String | - | 照会するセキュリティグループのテナントID |
| name | Query | String | - | 照会するセキュリティグループ名 |
| sort_dir | Query | Enum | - | 照会するセキュリティグループのソート方向<br>`sort_key`で指定したフィールドを基準にソート<br>**asc**、**desc**のいずれか |
| sort_key | Query | String | - | 照会するセキュリティグループのソートキー<br>`sort_dir`で指定した方向でソート |
| fields | Query | String | - | 照会するセキュリティグループのフィールド名<br>例) `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| security_groups | Body | Array | セキュリティグループリストオブジェクト |
| security_groups.tenant_id | Body | String | テナントID |
| security_groups.description | Body | String | セキュリティグループの説明 |
| security_groups.id | Body | UUID | セキュリティグループID |
| security_groups.security_group_rules | Body | Array | セキュリティグループルールリスト |
| security_groups.name | Body | String | セキュリティグループ名 |

<details><summary>例</summary>
<p>

```json
{
  "security_groups": [
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "description": "Default security group",
      "id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "security_group_rules": [
        {
          "direction": "ingress",
          "protocol": null,
          "description": "",
          "port_range_max": null,
          "id": "0c7279cd-657e-43cd-a635-6886ca3a8acd",
          "remote_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "remote_ip_prefix": null,
          "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
          "port_range_min": null,
          "ethertype": "IPv4"
        },
        {
          "direction": "egress",
          "protocol": null,
          "description": "",
          "port_range_max": null,
          "id": "4c5ae06e-44f0-4ea9-a999-29473873bca2",
          "remote_group_id": null,
          "remote_ip_prefix": null,
          "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
          "port_range_min": null,
          "ethertype": "IPv6"
        },
        {
          "direction": "egress",
          "protocol": null,
          "description": "",
          "port_range_max": null,
          "id": "4e21389a-bb3c-469c-8139-29da582bc3c5",
          "remote_group_id": null,
          "remote_ip_prefix": null,
          "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
          "port_range_min": null,
          "ethertype": "IPv4"
        },
        {
          "direction": "ingress",
          "protocol": null,
          "description": "",
          "port_range_max": null,
          "id": "72af180f-c425-4ec4-b7a3-90f86d4ce145",
          "remote_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "remote_ip_prefix": null,
          "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
          "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
          "port_range_min": null,
          "ethertype": "IPv6"
        }
      ],
      "name": "default"
    }
  ]
}
```

</p>
</details>

---

### セキュリティグループ表示
```
GET /v2.0/security-groups/{securityGroupId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 例 | 必須 | 説明 |
|---|---|---|---|---|
| securityGroupId | Query | UUID | O | 照会するセキュリティグループID |
| tokenId | Header | String | O | トークンID |
| fields | Query | String | - | 照会するセキュリティグループのフィールド名<br>指定したフィールドのみ返す<br>例) `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 例 | 説明 |
|---|---|---|---|
| security_group | Body | Object | セキュリティグループオブジェクト |
| security_group.tenant_id | Body | String | テナントID |
| security_group.description | Body | String | セキュリティグループの説明 |
| security_group.id | Body | UUID | セキュリティグループID |
| security_group.security_group_rules | Body | Array | セキュリティグループルールリスト |
| security_group.name | Body | String | セキュリティグループ名 |

<details><summary>例</summary>
<p>

```json
{
  "security_group": {
    "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
    "description": "Default security group",
    "id": "877b092c-2a31-4509-8d23-deeb02d95633",
    "security_group_rules": [
      {
        "direction": "ingress",
        "protocol": null,
        "description": "",
        "port_range_max": null,
        "id": "0c7279cd-657e-43cd-a635-6886ca3a8acd",
        "remote_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "remote_ip_prefix": null,
        "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv4"
      },
      {
        "direction": "egress",
        "protocol": null,
        "description": "",
        "port_range_max": null,
        "id": "4c5ae06e-44f0-4ea9-a999-29473873bca2",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv6"
      },
      {
        "direction": "egress",
        "protocol": null,
        "description": "",
        "port_range_max": null,
        "id": "4e21389a-bb3c-469c-8139-29da582bc3c5",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv4"
      }
      {
        "direction": "ingress",
        "protocol": null,
        "description": "",
        "port_range_max": null,
        "id": "72af180f-c425-4ec4-b7a3-90f86d4ce145",
        "remote_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "remote_ip_prefix": null,
        "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv6"
      }
    ],
    "name": "default"
  }
}
```

</p>
</details>

---

### セキュリティグループ作成

新しいセキュリティグループを作成します。新たに作成されたセキュリティグループは出る方向のセキュリティグループルールを基本的に含みます。

```
POST /v2.0/security-groups
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| security_group | Body | Object | O | セキュリティグループ作成リクエストオブジェクト |
| description | Body | String | - | セキュリティグループの説明 |
| name | Body | String | - | セキュリティグループ名 |

<details><summary>例</summary>
<p>

```json
{
    "security_group": {
        "name": "webservers",
        "description": "security group for webservers"
    }
}
```

</p>
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| security_group | Body | Object | セキュリティグループオブジェクト |
| security_group.tenant_id | Body | String | テナントID |
| security_group.description | Body | String | セキュリティグループの説明 |
| security_group.id | Body | UUID | セキュリティグループID |
| security_group.security_group_rules | Body | Array | セキュリティグループルールリスト |
| security_group.name | Body | String | セキュリティグループ名 |

<details><summary>例</summary>
<p>

```json
{
  "security_group": {
    "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
    "description": "security group for webservers",
    "id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
    "security_group_rules": [
      {
        "direction": "egress",
        "protocol": null,
        "description": null,
        "port_range_max": null,
        "id": "057e031a-ec2a-4bee-859a-6bc1d88c57d0",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv4"
      },
      {
        "direction": "egress",
        "protocol": null,
        "description": null,
        "port_range_max": null,
        "id": "cd37d4a7-75ac-4246-95cf-e93b37b75a9f",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv6"
      }
    ],
    "name": "webservers"
  }
}
```

</p>
</details>

---

### セキュリティグループ修正
セキュリティグループを修正します。
```
PUT /v2.0/security-groups/{securityGroupId}
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| securityGroupId | URL | UUID | O | セキュリティグループID |
| security_group | Body | Object | O | セキュリティグループ修正リクエストオブジェクト |
| description | Body | String | - | セキュリティグループの説明 |
| name | Body | String | - | セキュリティグループ名 |

<details><summary>例</summary>
<p>

```json
{
    "security_group": {
        "name": "new-webservers",
        "description": "security group for new webservers"
    }
}
```

</p>
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| security_group | Body | Object | セキュリティグループオブジェクト |
| security_group.tenant_id | Body | String | テナントID |
| security_group.description | Body | String | セキュリティグループの説明 |
| security_group.id | Body | UUID | セキュリティグループID |
| security_group.security_group_rules | Body | Array | セキュリティグループルールリスト |
| security_group.name | Body | String | セキュリティグループ名 |

<details><summary>例</summary>
<p>

```json
{
  "security_group": {
    "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
    "description": "security group for new webservers",
    "id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
    "security_group_rules": [
      {
        "direction": "egress",
        "protocol": null,
        "description": null,
        "port_range_max": null,
        "id": "057e031a-ec2a-4bee-859a-6bc1d88c57d0",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv4"
      },
      {
        "direction": "egress",
        "protocol": null,
        "description": null,
        "port_range_max": null,
        "id": "cd37d4a7-75ac-4246-95cf-e93b37b75a9f",
        "remote_group_id": null,
        "remote_ip_prefix": null,
        "security_group_id": "148cfc28-a58c-497f-aaab-c610bf7b5f18",
        "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
        "port_range_min": null,
        "ethertype": "IPv6"
      }
    ],
    "name": "new-webservers"
  }
}
```

</p>
</details>

---

### セキュリティグループ削除
指定したセキュリティグループを削除します。
```
DELETE /v2.0/security-groups/{securityGroupId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| securityGroupId | URL | UUID | O | セキュリティグループID |
| tokenId | Header | String | O | トークンID |

#### レスポンス
このAPIはレスポンス本文を返しません。

---

## セキュリティルール
### セキュリティルールリスト表示
```
GET /v2.0/security-group-rules
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| id | Query | UUID | - | 照会するセキュリティルールID |
| remote_group_id | Query | UUID | - | 照会するセキュリティルールの遠隔セキュリティグループID |
| protocol | Query | String | - | 照会するセキュリティルールのプロトコル |
| direction | Query | Enum | - | 照会するセキュリティルールが適用されるパケット方向<br>**ingress**または**egress** |
| ethertype | Query | Enum | - | 照会するセキュリティルールのネットワークトラフィック`Ethertype`値<br>**IPv4**または**IPv6** |
| port_range_max | Query | Integer | - | 照会するセキュリティルールのポート範囲最大値 |
| port_range_min | Query | Integer | - | 照会するセキュリティルールのポート範囲最小値 |
| security_group_id | Query | UUID | - | 照会するセキュリティルールが属すセキュリティグループID |
| tenant_id | Query | String | - | 照会するセキュリティルールのテナントID |
| remote_ip_prefix | Query | String | - | 照会するセキュリティルールの宛先IPアドレスプレフィックス |
| description | Query | String | - | 照会するセキュリティルールの説明 |
| sort_dir | Query | Enum | - | 照会するセキュリティルールのソート方向<br>`sort_key`で指定したフィールドを基準にソート<br>**asc**、**desc**のいずれか |
| sort_key | Query | String | - | 照会するセキュリティルールのソートキー<br>`sort_dir`で指定した方向でソート |
| fields | Query | String | - | 照会するセキュリティルールのフィールド名<br>例) `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| security_group_rules | Body | Array | セキュリティルールオブジェクトリスト |
| security_group_rules.direction | Body | Enum | セキュリティルールが適用されるパケット方向<br>**ingress**または**egress** |
| security_group_rules.ethertype | Body | Enum | セキュリティルールのネットワークトラフィック`Ethertype`値<br>**IPv4**または**IPv6** |
| security_group_rules.protocol | Body | String | セキュリティルールのプロトコル名 |
| security_group_rules.description | Body | String | セキュリティルールの説明 |
| security_group_rules.port_range_max | Body | Integer | セキュリティルールのポート範囲最大値 |
| security_group_rules.port_range_min | Body | Integer | セキュリティルールのポート範囲最小値 |
| security_group_rules.remote_group_id | Body | UUID | セキュリティルールの遠隔セキュリティグループID |
| security_group_rules.remote_ip_prefix | Body | Enum | セキュリティルールの宛先IPアドレスプレフィックス |
| security_group_rules.security_group_id | Body | UUID | セキュリティルールが属すセキュリティグループID |
| security_group_rules.tenant_id | Body | String | テナントID |
| security_group_rules.id | Body | UUID | セキュリティルールID |

<details><summary>例</summary>
<p>

```json
{
  "security_group_rules": [
    {
      "direction": "ingress",
      "protocol": "tcp",
      "description": "",
      "port_range_max": 65535,
      "id": "8eb7775f-1193-472a-98bd-e0599f94a64d",
      "remote_group_id": null,
      "remote_ip_prefix": "0.0.0.0/0",
      "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "port_range_min": 1,
      "ethertype": "IPv4"
    }
  ]
}
```

</p>
</details>

---

### セキュリティルール表示
```
GET /v2.0/security-group-rules/{securityGroupRuleId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| securityGroupRuleId | URL | UUID | O | セキュリティルールID |
| tokenId | Header | String | O | トークンID |
| fields | Query | String | - | 照会するセキュリティルールのフィールド名<br>例) `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| security_group_rule | Body | Object | セキュリティルールオブジェクト |
| security_group_rule.direction | Body | Enum | セキュリティルールが適用されるパケット方向<br>**ingress**または**egress** |
| security_group_rule.ethertype | Body | Enum | セキュリティルールのネットワークトラフィック`Ethertype`値<br>**IPv4**または**IPv6** |
| security_group_rule.protocol | Body | String | セキュリティルールのプロトコル名 |
| security_group_rule.description | Body | String | セキュリティルールの説明 |
| security_group_rule.port_range_max | Body | Integer | 照会するセキュリティルールのポート範囲最大値 |
| security_group_rule.port_range_min | Body | Integer | 照会するセキュリティルールのポート範囲最小値 |
| security_group_rule.remote_group_id | Body | UUID | セキュリティルールの遠隔セキュリティグループID |
| security_group_rule.remote_ip_prefix | Body | Enum | セキュリティルールの宛先IPアドレスプレフィックス |
| security_group_rule.security_group_id | Body | UUID | セキュリティルールが属すセキュリティグループID |
| security_group_rule.tenant_id | Body | String | テナントID |
| security_group_rule.id | Body | UUID | セキュリティルールID |

<details><summary>例</summary>
<p>

```json
{
  "security_group_rule": {
    "direction": "ingress",
    "protocol": "tcp",
    "description": "",
    "port_range_max": 65535,
    "id": "8eb7775f-1193-472a-98bd-e0599f94a64d",
    "remote_group_id": null,
    "remote_ip_prefix": "0.0.0.0/0",
    "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
    "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
    "port_range_min": 1,
    "ethertype": "IPv4"
  }
}
```

</p>
</details>

---

### セキュリティルール作成

新しいセキュリティグループルールを作成します。 IPv4に対するセキュリティルールのみ作成できます。

```
POST /v2.0/security-group-rules
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| security_group_rule | Body | Object | O | セキュリティルール作成リクエストオブジェクト |
| security_group_rule.remote_group_id | Body | UUID | - | セキュリティルールの遠隔セキュリティグループID |
| security_group_rule.direction | Body | Enum | O | セキュリティルールが適用されるパケット方向<br>**ingress**、**egress** |
| security_group_rule.ethertype | Body | Enum | - | `IPv4`に指定。省略時に`IPv4`に指定 |
| security_group_rule.protocol | Body | String | - | セキュリティルールのプロトコル名。省略時にすべてのプロトコルに適用。 |
| security_group_rule.port_range_max | Body | Integer | - | セキュリティルールのポート範囲最大値 |
| security_group_rule.port_range_min | Body | Integer | - | セキュリティルールのポート範囲最小値 |
| security_group_rule.security_group_id | Body | UUID | O | セキュリティルールが属すセキュリティグループID |
| security_group_rule.remote_ip_prefix | Body | Enum | - | セキュリティルールの宛先IPアドレスプレフィックス |
| security_group_rule.description | Body | String | - | セキュリティルールの説明 |

<details><summary>例</summary>
<p>

```json
{
    "security_group_rule": {
        "direction": "ingress",
        "port_range_min": "80",
        "ethertype": "IPv4",
        "port_range_max": "80",
        "protocol": "tcp",
        "remote_group_id": "85cc3048-abc3-43cc-89b3-377341426ac5",
        "security_group_id": "a7734e61-b545-452d-a3cd-0189cbd9747a"
    }
}
```

</p>
</details>

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| security_group_rule | Body | Object | セキュリティルールオブジェクト |
| security_group_rule.direction | Body | Enum | セキュリティルールが適用されるパケット方向<br>**ingress**または**egress** |
| security_group_rule.ethertype | Body | Enum | セキュリティルールのネットワークトラフィック`Ethertype`値<br>**IPv4**または**IPv6** |
| security_group_rule.protocol | Body | String | セキュリティルールのプロトコル名 |
| security_group_rule.description | Body | String | セキュリティルールの説明 |
| security_group_rule.port_range_max | Body | Integer | 照会するセキュリティルールのポート範囲最大値 |
| security_group_rule.port_range_min | Body | Integer | 照会するセキュリティルールのポート範囲最小値 |
| security_group_rule.remote_group_id | Body | UUID | セキュリティルールの遠隔セキュリティグループID |
| security_group_rule.remote_ip_prefix | Body | Enum | セキュリティルールの宛先IPアドレスプレフィックス |
| security_group_rule.security_group_id | Body | UUID | セキュリティルールが属すセキュリティグループID |
| security_group_rule.tenant_id | Body | String | テナントID |
| security_group_rule.id | Body | UUID | セキュリティルールID |

<details><summary>例</summary>
<p>

```json
{
  "security_group_rule": {
    "direction": "ingress",
    "protocol": "tcp",
    "description": "",
    "port_range_max": 65535,
    "id": "8eb7775f-1193-472a-98bd-e0599f94a64d",
    "remote_group_id": null,
    "remote_ip_prefix": "0.0.0.0/0",
    "security_group_id": "877b092c-2a31-4509-8d23-deeb02d95633",
    "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
    "port_range_min": 1,
    "ethertype": "IPv4"
  }
}
```

</p>
</details>

---

### セキュリティルール削除
指定したセキュリティルールを削除します。
```
DELETE /v2.0/security-group-rules/{securityGroupRuleId}
X-Auth-Token: {tokenId}
```

#### リクエスト
このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| securityGroupRuleId | URL | UUID | O | セキュリティルールID |
| tokenId | Header | String | O | トークンID |

#### レスポンス
このAPIはレスポンス本文を返しません。
