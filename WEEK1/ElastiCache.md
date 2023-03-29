# ElastiCache

high performance 와 low latency 를 제공하는 in-memory database service

- redis, memcached 를 지원함
- read query를 캐시해 부하를 줄일 수 있음.
- app의 state를 저장해 app을 stateless로 만들 수 있음

## Redis

- 고가용성
- 자동 장애 조치로 Multi-az 사용
- read replica를 통해 read scaling -> 가용성 올라감
- 백업과 복원 기능 있음

## Memcached

- 가용성 높지 않음
- 복제 발생 안함
- 백업, 복원 기능 없음

## 보안

- 모든 캐시는 IAM 인증을 지원 안함
- 레디스를 인증하려면 redis auth를 사용해야 함
- 전송 중 암호화를 위해 ssl 지원
- memcached는 SASL기반 인증 지원
