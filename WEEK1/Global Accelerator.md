# AWS Global Accelerator

## Unicast IP vs Anycast IP

- Unicast IP: 하나의 IP 주소를 하나의 서버에 할당
  - a서버는 12.34.56.78 b서버는 98.76.54.32
  - 일반적인 방식
- Anycast IP: 하나의 IP 주소를 여러 서버에 할당
  - a서버 b서버 둘 다 12.34.56.78
  - 클라이언트는 가장 가까운 서버로 라우팅 됨.

## AWS Global Accelerator 동작

- 가장 가까운 엣지 로케이션과 통신하고 엣지 로케이션은 내부 aws 네트워크를 통해 빠르게 ALB로 연결
- Global Accelerator는 두 개의 고정된 IP를 제공한다.

## CloudFront vs Global Accelerator

공통점

- 엣지 로케이션을 사용
- 가장 가까운 위치에서 액세스할 수 있도록 함
- AWS Shield를 사용하여 DDoS 공격을 방어

차이점

- CloudFront
  - 엣지로케이션에서 콘텐츠가 제공 됨
  - 이미지,비디오 같은 컨텐츠를 캐싱
- Global Accelerator
  - TCP/UDP를 상의 다양한 애플리케이션 성능을 향상
  - 비 HTTP를 사용할 경우 적합
  - 고정 IP를 요구하는 HTTP를 사용할 떄도 유용
