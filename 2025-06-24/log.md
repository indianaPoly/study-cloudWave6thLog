# 20250624 LOG


- UDP의 대표적 시스템

    Domain Name System (DNS)

- TCP 통신

    wireshark: tcp.flags.syn == 1 → SYN, ACK를 통해 3-way handshake 진행

    통신 종료 시: FIN, ACK를 활용하여 연결 종료

### Routing
- 기본 동작 : Router는 IP 목적지가 없으면 discard

- Static routing: 가는 값과 오는 값을 모두 설정해야 함

- Dynamic routing: RIP 사용

- Static Routing 예시
    ```
    VPC1(config)#ip route 172.31.1.0 255.255.255.0 2.2.12.2
    VPC1(config)#ip route 172.31.0.0 255.255.255.0 2.2.12.2

    라우팅 테이블에 저장된 값을 2개로 쓰는게 아니라 슈퍼네팅을 활용해서 하나로 바꿀 수 있다.

    VPC1(config)#ip route 172.31.0.0 255.255.254.0 2.2.12.2
    ```

- Default Route : S* 0.0.0.0/0 [1/0] via 2.2.12.6

    목적지를 모르면 2.2.12.6으로 보냄

### AWS VPC 관련
- 서브넷 생성 시 기본은 private subnet

    Public IPv4 주소 자동 할당을 설정해야 퍼블릭 서브넷으로 사용 가능

- 인터넷 게이트웨이는 VPC별 1개 생성 필요

- 동일 네트워크 서브넷 간 핑 → 방화벽(보안 그룹) 때문에 차단될 수 있음

- AS (Autonomous System)   
    AS = 망 식별 번호

    AWS BGP: AS 사이에서 사용

    IGP: AS 내에서 사용

- OSPF 설정 (Packet Tracer)
    ```
    VPC1
    router ospf 1
    network 172.16.0.0 0.0.0.255 area 0
    network 172.16.1.0 0.0.0.255 area 0
    network 2.2.12.0 0.0.0.3 area 0

    VPC2
    router ospf 1
    network 172.31.0.0 0.0.0.255 area 0
    network 172.31.1.0 0.0.0.255 area 0
    network 2.2.12.0 0.0.0.3 area 0
    ```

### GNS3
- Router 추가 시 router image 필요

- BGP 설정 : R1, R2 → 서로 다른 회사 간 BGP 설정