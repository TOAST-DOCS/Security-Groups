## Network > Security Groups > 개요

보안 그룹은 인스턴스의 송수신 트래픽을 제어하여 인스턴스를 보호할 목적으로 사용합니다. 규칙으로 지정한 트래픽은 허용하고, 나머지 트래픽은 차단하는 '포지티브 시큐리티 모델(positive security model)'을 사용합니다.
 
### 주요 기능
* 서비스를 처음 시작하면 기본 보안 그룹 하나가 생성되며, 유입되는 모든 트래픽을 차단합니다.
    * 따라서 'ping', 'ssh' 등의 서비스도 사용할 수 없으며 필요한 규칙을 설정해야만 사용할 수 있습니다.
    * 플로팅 IP를 사용한 외부 접근과 사설 IP를 사용한 내부 접근 모두에 동일하게 적용됩니다.
* 보안 그룹은 'stateful'로 동작하기 때문에 규칙으로 한 번 연결된 세션은 반대 방향의 규칙이 없더라도 허용됩니다.
    * 예를 들어 인스턴스로 향하는 TCP 80의 첫 번째 패킷이 '수신 TCP PORT 80' 규칙에 따라 통과되었다면, 인스턴스에서 TCP 80 포트를 출발지로 하여 전송되는 패킷은 차단되지 않습니다.
    * 다만, 일정 시간 규칙에 부합하는 패킷이 들어오지 않아 세션이 만료되면 반대 방향의 패킷도 차단됩니다.
* 기본 보안 그룹에는 인스턴스에서 나가는 모든 트래픽의 규칙이 설정되어 있습니다. 이 규칙을 삭제하지 않는다면, 인스턴스로부터 시작되는 세션은 모두 허용됩니다.
* 인스턴스에는 다수의 보안 그룹을 설정할 수 있습니다.
* 규칙은 하나씩 추가하는 것보다 범위를 지정하는 것이 효율 면에서 유리합니다. 규칙이 증가하면 성능 저하가 발생할 수 있습니다.
* 세션의 상태가 맞지 않는 트래픽은 차단될 수 있습니다.
* IP 프로토콜 목록에 없는 규칙은 정의하여 사용할 수 있습니다.
