## Network > Security Groups > API v2 Guide

API를 사용하려면 API 엔드포인트와 토큰 등이 필요합니다. [API 사용 준비](/Compute/Compute/ko/identity-api/)를 참고하여 API 사용에 필요한 정보를 준비합니다.

보안 그룹 API는 `network` 타입 엔드포인트를 이용합니다. 정확한 엔드포인트는 토큰 발급 응답의 `serviceCatalog`를 참조합니다.

| 타입 | 리전 | 엔드포인트 |
|---|---|---|
| network | 한국(판교) 리전<br>한국(평촌) 리전<br>일본 리전 | https://kr1-api-network.infrastructure.cloud.toast.com<br>https://kr2-api-network.infrastructure.cloud.toast.com<br>https://jp1-api-network.infrastructure.cloud.toast.com |

API 응답에 가이드에 명시되지 않은 필드가 나타날 수 있습니다. 이런 필드는 NHN Cloud 내부 용도로 사용되며 사전 공지 없이 변경될 수 있으므로 사용하지 않습니다.


## Security Group
### List Security Groups
```
GET /v2.0/security-groups
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | Security group ID to query |
| tenant_id | Query | String | - | Tenant ID of security group to query |
| name | Query | String | - | Name of security group to query |
| sort_dir | Query | Enum | - | Sorting direction of security group to query <br>Sort by the field specified by`sort_key`<br>Either **asc** or **desc** |
| sort_key | Query | String | - | Sorting key of security group to query <br>Sort in the direction as specified by`sort_dir` |
| fields | Query | String | - | Field name of security group to query <br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_groups | Body | Array | Object of security group list |
| security_groups.tenant_id | Body | String | Tenant ID |
| security_groups.description | Body | String | Description of security group |
| security_groups.id | Body | UUID | Security group ID |
| security_groups.security_group_rules | Body | Array | List of security group rules |
| security_groups.name | Body | String | Security group name |

<details><summary>Example</summary>
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

### Get Security Group
```
GET /v2.0/security-groups/{securityGroupId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| securityGroupId | Query | UUID | O | ID of security group to query |
| tokenId | Header | String | O | Token ID |
| fields | Query | String | - | Field name of security group to query <br>Return specified fields only to response <br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_group | Body | Object | Security group object |
| security_group.tenant_id | Body | String | Tenant ID |
| security_group.description | Body | String | Security group description |
| security_group.id | Body | UUID | Security group ID |
| security_group.security_group_rules | Body | Array | List of security group rules |
| security_group.name | Body | String | Security group name |

<details><summary>Example</summary>
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

### Create Security Group

Create a new security group: new security group, by default, includes the egress security group rules.

```
POST /v2.0/security-groups
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| security_group | Body | Object | O | Object requesting of creating security group |
| description | Body | String | - | Security group description |
| name | Body | String | - | Security group name |

<details><summary>Example</summary>
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

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_group | Body | Object | Security group object |
| security_group.tenant_id | Body | String | Tenant ID |
| security_group.description | Body | String | Security group description |
| security_group.id | Body | UUID | Security group ID |
| security_group.security_group_rules | Body | Array | List of security group rules |
| security_group.name | Body | String | Security group name |

<details><summary>Example</summary>
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

### Modify Security Group
Modify an existing security group.
```
PUT /v2.0/security-groups/{securityGroupId}
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| securityGroupId | URL | UUID | O | Security group ID |
| security_group | Body | Object | O | Object requesting of modifying security group |
| description | Body | String | - | Security group description |
| name | Body | String | - | Security group name |

<details><summary>Example</summary>
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

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_group | Body | Object | Security group object |
| security_group.tenant_id | Body | String | Tenant ID |
| security_group.description | Body | String | Security group description |
| security_group.id | Body | UUID | Security group ID |
| security_group.security_group_rules | Body | Array | List of security group rules |
| security_group.name | Body | String | Security group name |

<details><summary>Example</summary>
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

### Delete Security Group
Delete specified security group. 
```
DELETE /v2.0/security-groups/{securityGroupId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body. 

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| securityGroupId | URL | UUID | O | Security group ID |
| tokenId | Header | String | O | Token ID |

#### Response
This API does not return a response body. 

---

## Security Rule
### List Security Rules 
```
GET /v2.0/security-group-rules
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body. 

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| id | Query | UUID | - | Security rule ID to query |
| remote_group_id | Query | UUID | - | Remote security group ID of security rule to query |
| protocol | Query | String | - | Protocol of security rule to query |
| direction | Query | Enum | - | Packet direction to which security rule to query is applied<br>**ingress** or **egress** |
| ethertype | Query | Enum | - | The `Ethertype` value of network traffic of security rule to query<br>**IPv4** or **IPv6** |
| port_range_max | Query | Integer | - | Maximum value within port range of security rule to query |
| port_range_min | Query | Integer | - | Minimum value within port range of security rule to query |
| security_group_id | Query | UUID | - | Security group ID including security rule to query |
| tenant_id | Query | String | - | Tenant ID of security rule to query |
| remote_ip_prefix | Query | String | - | Prefix of destination IP of security rule to query |
| description | Query | String | - | Description of security rule to query |
| sort_dir | Query | Enum | - | Sorting direction of security rule to query <br>Sort by the field specified by `sort_key`<br>Either **asc** or **desc** |
| sort_key | Query | String | - | Sorting key of security rule to query <br>Sort in the direction specified by `sort_dir` |
| fields | Query | String | - | Field name of security rule to query<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_group_rules | Body | Array | List of security rule objects |
| security_group_rules.direction | Body | Enum | Packet direction to which security rule is applied <br>**ingress** or **egress** |
| security_group_rules.ethertype | Body | Enum | The `Ethertype` value of network traffic of security rule <br>**IPv4** or **IPv6** |
| security_group_rules.protocol | Body | String | Protocol name of security rule |
| security_group_rules.description | Body | String | Security rule description |
| security_group_rules.port_range_max | Body | Integer | Maximum value within port range of security rule |
| security_group_rules.port_range_min | Body | Integer | Minimum value within port range of security rule |
| security_group_rules.remote_group_id | Body | UUID | Remote security group ID of security rule |
| security_group_rules.remote_ip_prefix | Body | Enum | Prefix of destination IP of security rule |
| security_group_rules.security_group_id | Body | UUID | Security group ID including security rule |
| security_group_rules.tenant_id | Body | String | Tenant ID |
| security_group_rules.id | Body | UUID | Security rule ID |

<details><summary>Example</summary>
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

### Get Security Rule
```
GET /v2.0/security-group-rules/{securityGroupRuleId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body. 

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| securityGroupRuleId | URL | UUID | O | Security rule ID |
| tokenId | Header | String | O | Token ID |
| fields | Query | String | - | Field name of security rule to query <br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| security_group_rule | Body | Object | Security rule object |
| security_group_rule.direction | Body | Enum | Packet direction to which security rule is applied<br>**ingress** or **egress** |
| security_group_rule.ethertype | Body | Enum | The  `Ethertype` value of network traffic of security rule <br>**IPv4** or **IPv6** |
| security_group_rule.protocol | Body | String | Protocol name of security rule |
| security_group_rule.description | Body | String | Security rule description |
| security_group_rule.port_range_max | Body | Integer | Maximum value within port range of security rule to query |
| security_group_rule.port_range_min | Body | Integer | Minimum value within port range of security rule to query |
| security_group_rule.remote_group_id | Body | UUID | Remote security group ID of security rule |
| security_group_rule.remote_ip_prefix | Body | Enum | Prefix of destination IP of security rule |
| security_group_rule.security_group_id | Body | UUID | Security group ID including security rule |
| security_group_rule.tenant_id | Body | String | Tenant ID |
| security_group_rule.id | Body | UUID | Security rule ID |

<details><summary>Example</summary>
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

### Create Security Rule

Create a new security group rule. It is available to create security rules only for IPv4. 

```
POST /v2.0/security-group-rules
X-Auth-Token: {tokenId}
```

#### Request	

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| security_group_rule | Body | Object | O | Object requesting of creating security rules |
| security_group_rule.remote_group_id | Body | UUID | - | Remote security group ID of security rule |
| security_group_rule.direction | Body | Enum | O | Packet direction to which security rule is applied<br>**ingress**, **egress** |
| security_group_rule.ethertype | Body | Enum | - | If left blank, specified with`IPv4`. |
| security_group_rule.protocol | Body | String | - | Protocol name of security rule: to be applied to all protocols, if it is omitted. |
| security_group_rule.port_range_max | Body | Integer | - | Maximum value within port range of security rule |
| security_group_rule.port_range_min | Body | Integer | - | Minimum value within port range of security rule |
| security_group_rule.security_group_id | Body | UUID | O | ID of security group including security rules |
| security_group_rule.remote_ip_prefix | Body | Enum | - | Prefix of destination IP of security rule |
| security_group_rule.description | Body | String | - | Security rule description |

<details><summary>Example</summary>
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

#### Response	

| Name | Type | Format | Description |
|---|---|---|---|
| security_group_rule | Body | Object | Security rule object |
| security_group_rule.direction | Body | Enum | Packet direction to which security rules are applied <br>**ingress** or **egress** |
| security_group_rule.ethertype | Body | Enum | The `Ethertype` of network traffic of security rules <br>**IPv4** or **IPv6** |
| security_group_rule.protocol | Body | String | Protocol name of security rule |
| security_group_rule.description | Body | String | Security rule description |
| security_group_rule.port_range_max | Body | Integer | Maximum value within port range of security rule to query |
| security_group_rule.port_range_min | Body | Integer | Minimum value within port range of security rule to query |
| security_group_rule.remote_group_id | Body | UUID | ID of remote security group of security rule |
| security_group_rule.remote_ip_prefix | Body | Enum | Prefix of destination IP of security rule |
| security_group_rule.security_group_id | Body | UUID | ID of security group including security rule |
| security_group_rule.tenant_id | Body | String | Tenant ID |
| security_group_rule.id | Body | UUID | Security rule ID |

<details><summary>Example</summary>
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

### Delete Security Rule
Delete a specified security rule.
```
DELETE /v2.0/security-group-rules/{securityGroupRuleId}
X-Auth-Token: {tokenId}
```

#### Request
This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| securityGroupRuleId | URL | UUID | O | ID of security rules |
| tokenId | Header | String | O | Token ID |

#### Response
This API does not return a request body. 
