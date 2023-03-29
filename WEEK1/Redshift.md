# Amazon Redshift

- Amazon Redshift는 데이터를 저장하고 분석하기 위한 데이터 웨어하우스 서비스
- 다른 데이터 웨어하우징보다 성능이 10배 이상 좋고 데이터가 PB 규모로 확장되므로 대규모 데이터 분석에 적합
- Multi-AZ 없음
- 재해복구전략을 위해 스냅샷 사용

## 데이터 로드

- Kinesis Data Firehose
- S3 using COPY command
- EC2 Instance JDBC driver
