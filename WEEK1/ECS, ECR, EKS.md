# Amazon ECS(Elastic Container Service)

컨테이너를 쉽게 배포,관리, 스케일링할 수 있도록 도와주는 완전 관리형 컨테이너 오케스트레이션 서비스

## EC2 Launch Type

- 클러스터에서 ec2 인스턴스를 구성하고 배포하여 컨테이너를 실행
- 지속적으로 높은 CPU 코어 및 메모리 사용량이 필요한 워크로드
- 가격에 최적화되어야 하는 대규모 워크로드
- 애플리케이션이 영구 스토리지에 액세스해야 함
- 인프라를 직접 관리해야 함

## Fargate Launch Type

- 서버리스 종량제 옵션, 인프라 관리 필요 없이 컨테이너 실행
- 낮은 오버헤드를 위해 최적화해야 하는 대규모 워크로드
- 가끔 버스트가 발생하는 소규모 워크로드
- 작은 워크로드
- 배치 워크로드

## ECS Auto Scaling

- Target Tracking
- Step Scaling
- Scheduled Scaling

EC2 Auto Scaling이 필요하지 않다면 Faregate를 사용하는 것이 좋다.

# Amazon ECR(Elastic Container Registry)

- AWS에 도커 이미지를 저장하고 관리하는 저장소
- 계정에 한해 private 저장소를 생성할 수 있음
- public 저장소에 개시하는 것도 가능
- ECR은 단순히 저장소에 그치지 않고 취약점 스캐닝, 버저닝 태그 및 수명 주기 확인도 지원
- ECS와 통합해 사용 가능

# Amazon EKS(Elastic Kubernetes Service)

- AWS에 관리형 kubernetes 서비스

## Node Types

- Managed Node Group
  - EKS에서 관리
  - 온디맨드, 스팟 인스턴스 지원
- Self Managed Node Group
  - 사용자 지정
  - 사전 빌드된 AMI 사용해 시간 절약 가능
  - 온디맨드, 스팟 인스턴스 지원
- Fargate
- 노드를 원치 않는 경우 Fargate 사용

## Data Volumes

- EKS Cluster에 스토리지 클래스 매니페스트 지정
- Container Storage Interface(CSI) 드라이버를 사용
