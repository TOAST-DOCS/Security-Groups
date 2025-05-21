## Network > Security Groups > Console User Guide

## Security Management Group

### Creating security groups
A default security group is created when the service is launched for the first time, and additional security groups can be created afterwards.
When a security group is created, a rule for all outgoing traffic is added unconditionally. This rule can be changed or deleted in the Security Group Rule Settings.
Even if the security group has been created, the rule will not be applied unless you set the security group for the instance.


### Create Security Rules
Create rules to apply to the security group. You can create multiple security rules for a single security group. If a security group is set for an instance, all security rules created in the security group are applied.

| Item        | Description                                                         |
| ----------- | ------------------------------------------------------------ |
| Direction        | Ingress means the direction into the instance. Egress means the direction going out of the instance. |
| Ether Type  | It means the version of the EtherType IP. IPv4 or IPv6 can be specified. |
| IP protocol | You can specify a specific protocol or specify all. Another protocol 0 means 'random', and it allows all IP protocols.       |
| Port range   | For L4 protocol, the port range can be specified.         |
| Remote        | You can specify a security group or IP address range. If the rule direction is 'egress', the destination is remote; if it is 'ingress', the source is remote. <br>The source and destination of traffic are compared in consideration of the rule direction. If you specify a security group, it compares whether the address is the IP address of an instance that belongs to the specified security group. <br>If you select CIDR to specify an IP address or range, it compares if the address is the configured IP address or range. |
| Description        | You can add description for security group rules.          |

### 보안 규칙 대량 생성
제공되는 템플릿 파일에 보안 그룹 규칙들을 기재한 후 이를 업로드하여 최대 300개의 보안 그룹 규칙을 한번에 생성할 수 있습니다.

> [참고]
> TCP, ICMP, UDP 프로토콜을 추가할 때 포트 범위를 입력하지 않으면 전체 포트 범위(ALL)로 적용됩니다.
> 대량 생성 템플릿의 설명 영역(1~8행)을 삭제하면 업로드가 정상적으로 처리되지 않습니다.

### 보안 규칙 목록 다운로드
보안 그룹에 설정된 보안 규칙 목록을 파일로 다운로드할 수 있습니다.

### Applying security groups
If you select a security group when you create an instance, the security group is applied. Multiple security groups can be set on the instance. The rules of all set security groups are applied to the instance.
For example, if the security group 'CONN' has rules 'Ingress TCP PORT 22' and 'Ingress TCP PORT 23', and the security group 'WEB' has rules 'Ingress TCP PORT 80' and 'Ingress TCP PORT 8080', setting two security groups 'CONN' and 'WEB' on a single instance will apply all four rules, allowing you to use all of the services.
The security groups that were applied to the instance can be changed in the Instance Management menu. The identical security group can be applied to a number of instances. 

