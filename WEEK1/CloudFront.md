# AWS CloudFront

- CloudFront란 AWS에서 제공하는 CDN(Content Delivery Network)이다.

- 웹사이트 컨텐츠를 서로 다른 edge location에 미리 캐싱해서 read 성능을 높이는 것이다.

- 컨텐츠가 네트워크 전체에 캐싱되므로 사용자가 낮은 레이턴시로 접근 가능

- DDos 방어 가능

1. 클라이언트가 엣지 로케이션으로 요청
2. 엣지는 캐싱되어있는지 확인 -> 있으면 응답
3. 없으면 private network로 원본에 요청 -> 결과를 로컬에 저장 후 같은 컨텐츠를 다음 요청시 같은 엣지에서 응답

## CRR(교차 리전 복제)

- CloudFront는 글로벌 엣지 네트워크를 이용하는데 CRR은 복제를 원하는 리전에 설정을 따로 해야 함.
- 실시간으로 갱신되며 읽기 전용으로만 설정 가능
- 일부 리전을 대상으로 동적 컨텐츠를 낮은 지연 시간으로 제공하고자 할때 사용

## CloudFront Geo Restriction

- 사용자들의 지리적 위치를 기반으로 컨텐츠를 제한할 수 있다.
- 접근이 가능한 국가 목록을 만들거나, 반대 케이스도 가능, 저작권법으로 인한 제한

## CloudFront Pricing

- 엣지 로케이션마다 다른 요금이 적용된다.

- Price Classes
  - Price Class All: 모든 리전 사용, 최고 성능, 비쌈
  - Price Class 200: 200개 이상의 엣지 로케이션 사용, 중간 성능, 중간 가격
  - Price Class 100: 100개 이상의 엣지 로케이션 사용, 최저 성능, 저렴

## CloudFront Cache Invalidation

- 특정 파일에 대한 업데이트 사항이 최대한 빨리 반영되길 원할 때 캐시 무효화를 사용
- index.html 같은 특정 파일을 무효화 하거나 /images/\* 같은 모든 이미지 파일을 무효화 할 수 있다.
