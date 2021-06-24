## Network > Security Groups > Overview

The security group controls the ingress and egress traffic of the instance and use them to protect the instance. It allows traffic specified under the policy, and uses '(positive security model)' to block the rest of the traffic.

### Key Features
* A default security group is created when the service begins for the first time to block all ingress traffic. 
  * Therefore, services such as 'ping' and 'ssh' cannot be used unless necessary policies are set. 
  * It is identically applied for both the external access using the floating IP and the internal access using the private IP. 
* The security group operates as 'stateful', so the session which was once connected with the policy will be allowed even if it does not have any policy in the opposite direction. 
  * For example, the first packet of instance-bound TCP 80 has passed the 'Ingress TCP PORT 80' policy, the packet being sent by making the TCP 80 port as the starting point will not be blocked. 
  * But if the session expires because the packet which satisfies the policies for a certain period of time does not come in, the packet in the opposite direction is blocked as well.
* In the default security group, the policy for all outgoing traffic has been set. If you do not delete this policy, all sessions that start from the instance will be allowed.
* In the instance, many security groups can be set.
* It is more efficient to set the range rather than adding a policy one by one. If the number of polices increases, it may lead to performance degradation.
* Sessions with invalid state can be blocked.
* Policies not in the IP protocol list can be defined and used. [Well-known port](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)

