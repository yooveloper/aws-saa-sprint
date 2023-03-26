# ELB 및 ASG

## 고가용성 및 스케일링성(Scalability & High Availability)

확장성은 애플리케이션 시스템이 조정을 통해 더 많은 양을 처리할 수 있다는 의미이다.

확장성에는 수직적 확장과 수평적 확장이 있다.

### 수직적 확장성(Vertical Scalability)

- 인스턴스의 크기를 확장하는 것을 의미
- 예를들면 t2.micro를 쓰다가 t2.large로 바꾸는 것
- 데이터베이스와 같은 분산되지 않은 환경에서 일반적으로 선택(RDS, ElastiCache)
- 하드웨어의 제한으로 인해 확장의 한계가 있음
- 스케일 업 / 다운

<br >

### 수평적 확장성(Horizontal Scalability)

- 인스턴스나 시스템의 수를 늘리는 방법
- 예를들면 한명이 하던 업무를 두명이서 처리
- 수평 확장을 했다는 건 분배 시스템이 있다는 걸 의미한다.
- 스케일 아웃 / 인

<br>

### 고가용성(High Availability)

- 고가용성이란 애플리케이션 또는 시스템이 적어도 둘 이상의 AWS의 AZ나 데이터 센터에서 가동 중이라는걸 의미한다.
- 고가용성의 목표는 데이터 센터의 손실에서 살아남는 것.

<br >

## 로드 밸런싱(Load Balancing)

여러 대의 서버나 인스턴스 간의 트래픽을 분산하여 애플리케이션의 가용성과 확장성을 향상시키는 기술이다.

애플리케이션의 부하 분산과 장애 대응 등 다양한 이점을 제공한다.

### AWS ELB(Elastic Load Balancing)

HTTP를 다루는 애플리케이션 레이어의 로드밸런서이다.(L7)

ELB를 사용하면 여러 EC2 인스턴스 간의 트래픽을 분산시켜 서비스의 가용성과 확장성을 높일 수 있다.

ELB는 다음과 같은 유형이 있다.

### ALB(Application Load Balancer)

- HTTP 및 HTTPS 트래픽을 분산시켜 EC2 인스턴스 또는 컨테이너로 트래픽을 전달하는 로드 밸런서이다.
- 다중 가용 영역에서 실행되므로, 하나 이상의 가용 영역에서 장애가 발생해도 서비스 중단이 최소화 된다.
- SSL/TLS 암호화를 지원한다.
- HTTP2, WebScoket 지원
- redirect를 지원하므로 HTTP를 HTTPS로 리다이렉트 하는걸 로드밸런스 단에서 구현할 수 있음
- URL 대상 경로에 기반한 라우팅 지원
  - example.com/users & example.com/posts
- hostname 기반 라우팅 지원
  - one.example.com & other.example.com
- Query String 기반 라우팅 지원
  - example.com/users?region=us-east-1
- 마이크로 서비스나 컨테이너 기반 애플리케이션에 가장 좋은 로드 밸런서이다.
- 포트 매핑 기능이 있어 ECS 인스턴스의 동적 포트로의 리다이렉션을 지원한다.

### ALB Target Groups

- EC2 인스턴스
- ECS tasks
- Labmda functions
- IP 주소 앞에도 위치할 수 있음 (사설 IP만)
- 상태확인은 대상 그룹 레벨에서만 이뤄진다.

<br >

### NLB(Network Load Balancer)

네트워크 레이어의 로드 밸런서이다.(L4)

L4 로드 밸런서이므로 TCP와 UDP 트래픽을 다룰 수 있다.

시험에서 TCP,UDP가 나오면 L4 로드밸런서를 떠올려라.

- 초당 수백만 건 처리 가능하고 L7 로드 밸런서보다 더 낮은 지연 시간을 제공한다.
  - ALB는 400ms, NLB는 100ms
- 가용 영역별로 하나의 고정 IP를 가진다.
  - 여러개의 고정 IP를 가진 애플리케이션을 노출할 때 유용하다.
  - 탄력적 IP 도 사용 가능
  - 1 ~ 3개의 IP로만 액세스할 수 있는 app을 만들라는 문제가 나오면 NLB도 고려해보자.
- 고성능, TCP, UDP, 정적IP가 나오면 NLB를 생각해라.

### NLB Target Groups

- EC2 인스턴스
- IP 주소
  - 반드시 하드코딩 되어야 하고, private Ip여야 한다.
- ALB 앞에 NLB를 사용할 수도 있다.
  - 이렇게 사용하는 이유는 NLB 덕분에 고정 IP를 얻을 수 있고, ALB 덕분에 HTTP 트래픽을 처리하는 규칙을 얻을 수 있다.
- 상태확인(Health Check)를 지원하는 프로토콜은 TCP, HTTP, HTTPS 이다.
