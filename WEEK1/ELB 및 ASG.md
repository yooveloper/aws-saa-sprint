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

<br >

## Gateway Load Balancer(GWLB)

네트워크 계층(3계층) 에서 동작하는 로드밸런서로서

모든 로드 밸런서보다 낮은 계층에서 실행된다.

### GWLB의 두 가지 기능

- Transparent Network Gateway(투명 네트워크 게이트웨이): 모든 트래픽에 대한 단일 진입/출구
- target group의 appliances 집합에 트래픽을 분산한다.
- 시험 볼때 6081 포트의 GENEVE 프로토콜을 사용해라.

<br >

### GWLB의 target group

- EC2 instance
- IP Address - must be private IPs

<br >

## Sticky Session

분산된 서버 인스턴스 구조에서

a 클라이언트가 최초에 a 인스턴스로 요청을 보냈다면

로드밸런서에서 두 번째 요청을 실행할 때 a 클라이언트의 요청은 a 인스턴스로만 가게 하는걸 스티키 세션이라고 한다.

- 일부 인스턴스는 고정 유저를 갖게 되고 인스턴스의 부하가 발생할 수 있음.

sticky session 에는 두 가지 쿠키가 있다.

- Application-based Cookies
  - Custom cookie(사용자 정의 쿠키)
    - 앱에 필요한 데이터를 포함할 수 있음
    - AWSALB, AWSALBAPP 과 같은 이름 사용하면 안됨 (ELB에서 사용함)
  - Application cookie
    - 로드밸런서에서 자체 생성
    - ALB의 쿠키 이름은 `AWSALBAPP`
  - 애플리케이션에서 기간을 지정할 수 있음
- Duration-based Coockies
  - 로드밸런서에서 생성되는 쿠키
  - ALB에서는 이름이 `AWSALB` 이다.
  - 특정 기간을 기반으로 만료되며 기간은 로드밸런서에서 자체적으로 정한다.

<br >
<br >
<br >

## Cross-Zone Load Balancing

- Cross-Zone Load Balacing을 사용하면 모든 영역에 있는 EC2 인스턴스에 트래픽이 고르게 분산된다.
- ALB는 Cross-Zone Load Balancing이 default로 활성화되어있다.
- AZ 간의 데이터 이동에 비용이 들지 않는다.
- NLB와 GWLB는 Cross-Zone Load Balancing이 기본적으로 비활성화 되어 있다.
  - AZ 간에 데이터 이동 시 비용 지불

## Connection Draining

ALB & NLB를 사용할 경우 Deregiestration Delay(등록 취소 지연) 이라고 한다

인스턴스가 등록 취소, 혹은 비정상적인 상태에 있을 때 어느정도 딜레이를 줘서 활성 요청을 완료할 수 있도록 하는 기능

연결이 드레이닝 되면 ELB는 등록 취소중인 인스턴스로 더이상 요청을 보내지 않는다.

쉽게 말하면 걍 사용자의 요청을 처리중인 인스턴스를 바로 삭제 못하게 하는 기능인듯?

예를들어 사용자 수가 줄어들면 auto scaling이 인스턴스를 지우려고 할텐데 이때 사용자가 해당 인스턴스에서 무언가 작업을 하고 있으면 지우기전에 해당 요청을 완료할 수 있도록
지정한 시간 만큼 기다리는 기능이다.

1~3600 seconds 까지 설정 가능하고 default는 300s 이다.

<br >
<br >
<br >

# Auto Scaling Group(ASG)

- 트래픽에 대응해서 자동으로 인스턴스를 스케일 in-out 해주는 기능
- minimum, maximum capacity를 parameter로 설정할 수 있다.
- 로드밸런서와 페어링 할 경우 ASG에 속한 모든 ec2 인스턴스가 자동으로 로드밸런서에 연결 됨.
- 한 인스턴스가 비정상이면 종료하고 새 인스턴스를 생성함.
- ASG는 무료이고 ec2 인스턴스와 같은 하위 리소스에 대한 비용만 내면 된다.

## ASG Attributes

- Launch Template
  - AMI + instance type
  - EC2 User Data
  - EBS Volume
  - Security Group
  - SSH key pair
  - IAM Roles for your instance
  - Network + Subnets information
  - load balancer information
- Min size / Max size / initial Capacity
- Scaling Policies

## CloudWatch Alarms & Scaling

- 클라우드 와치 알림 기반으로 scale in/out 할 수 있다.
  - CPU 사용량이나 특정 유저 수 등의 metric으로 트리거를 발동

<br >
<br >

## ASG Scaling Policies

### Dynamic Scaling Policies

- Target Tracking Scaling(대상 추적)

  - 가장 단순하고 설정하기 쉬움
  - 예를들어 CPU 사용량을 40% 기준선으로 정하고 스케일링 하는 등

- Simple / Step Scaling

  - CloudWatch Alarm을 기반으로 스케일링
  - CPU 사용량이 늘어나면 2대의 unit을 추가 한다거나
  - 반대로 30% 아래로 내려가면 1대의 unit을 remove

- Scheduled Actions

  - 예정된 스케줄을 바탕으로 스케일링
  - 예를들어 우리 서비스가 금요일 오후 5시에 큰 이벤트가 있으니까 그때를 대비해 min capacity를 늘린다던가 하는 식으로 사용

- Predictive Scaling(예측 스케일링)
  - 과거 로드 데이터를 분석해서 예측을 하고 해당 예측을 기반으로 사전에 스케일링 작업 예약

### Good metrics to scale on

- CPUUtilization: Average CPU
- RequestCountPerTarget
- Average Network I/O
- Custom metrics

### Scaling Cooldowns

- 스케일링 작업이 끝날 때마다 인스턴스의 추가/삭제를 막론하고 기본적으로 300초를 쉬는 것
- Cooldown 기간에는 ASG가 추가 인스턴스를 실행/종료 할 수 없음
- 이는 새로운 인스턴스의 안정화 + 새로운 지표의 양상을 파악하기 위해 존재
- Scaling이 발생할때 Cooldown이 설정되어 있는지 확인해야 함.
- AMI 를 사용해서 ec2 인스턴스 구성 시간을 단축하면 더 많은 동적 스케일링이 가능함
