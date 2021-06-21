## Network > Security Groups > Console User Guide

## Security Management Group

### Creating security groups
A default security group is created when the service is launched for the first time, and additional security groups can be created afterwards.
A policy must be added for all traffic sent when the security group was created. This policy can be changed or deleted in the Security Group Policy Settings.
Even if the security group was created, the policy will not apply if the security group is not set for the instance.


### Creating security policies
Create a policy to apply to the security group. A number of security policies can be created for a single security group. If a security group is set for the instance, all security policies created in the security group will be applied.

| Item        | Description                                                         |
| ----------- | ------------------------------------------------------------ |
| Direction        | Ingress means the direction into the instance. Egress means the direction going out of the instance. |
| Ether Type  | It means the version of the EtherType IP. IPv4 or IPv6 can be specified. |
| IP protocol | You can specify a specific protocol or specify all. Another protocol 0 means 'random', and it allows all IP protocols.       |
| Port range   | For L4 protocol, the port range can be specified.         |
| Remote        | The security group or IP address range can be specified. If the policy direction is 'egress', the destination is remote; if 'ingress', the starting point is remote. <br>The starting point and destination are compared in consideration of the policy direction. If the security group is specified, it compares if it is the IP of an instance which belongs to the specific security group.  <br>If the CIDR was selected to specify the IP address or range, it compares if it is the set IP address or range. |
| Description        | You can add description for security group policies.         |


### Applying security groups
If a security group is selected when creating an instance, the security group is applied. In the instance, many security groups can be set. The policies of all set security groups are applied to the instance.
For example, if the security group 'CONN' has policies 'Ingress TCP PORT 22', 'Ingress TCP PORT 23', and the security group 'WEB' has policies such as 'Ingress TCP PORT 80', 'Ingress TCP PORT 8080', setting two security groups ('CONN', 'WEB') to a single instance will apply all four policies, allowing you to use all of the services.
The security groups that were applied to the instance can be changed in the Instance Management menu. The identical security group can be applied to a number of instances.
