# VPC(Virtual Private Cloud)

- 독립된 가상의 클라우드 네트워크 환경을 제공하는 AWS 서비스
- VPC 내에서 IP대역, 서브넷, 라우팅 테이블, 인터넷 게이트웨이, 보안 그룹, ACL 등을 생성 및 제어
- subnet은 하나의 az안에 종속되어야 한다.

## Public Subnet & Private Subnet

VPC 안에 구성할 수 있는 서브넷 구성에는 Public Subnet과 Private Subnet이 있다.

- Public Subnet
  - 외부와 자유로운 통신이 가능
- Private Subnet
  - 외부에서 직접 접근 불가
  - NAT Gateway를 이용해 내부 -> 외부로 단방향 통신 가능

## CIDR

- CIDR은 IP 범위
  - 추후 정리

## VPC Peering

- Private IPv4, IPv6 주소를 사용하여 VPC 끼리 연결

## VPC Endpoint

- VPC 내부에서 AWS 서비스에 접근할 수 있도록 하는 서비스
