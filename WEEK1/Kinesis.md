# Amazon Kinesis

실시간 스트리밍 데이터 서비스

## Kinesis Data Streams

- 대규모 데이터를 실시간으로 수집하고 처리
- 보존기간 1~365일
- 데이터 재처리, 확인 가능
- kinesis로 데이터가 들어오면 삭제 불가

- Producers(데이터를 전송하는 클라이언트)
  - 레코드는 Partition Key와 Data Blob(최대 1mb)로 구성
  - Partition Key는 샤드를 결정하는데 사용, 블롭은 값 자체를 의미
  - 데이터끼리 같은 Partition Key를 가지면 같은 샤드에 저장
  - 생산자가 데이터를 스트림으로 보낼 때 초당 1mb를 전송하거나 샤드당 1초에 천 개의 메시지를 전송 가능
    - 여섯 개의 샤드가 있다면 초당 6mb, 총 6천개의 메시지를 얻을 수 있다.
- Consumers(소비자)
  - KCL, Lambda, Kinesis Data Firehose, Kinesis Data Analytics 등을 사용하여 데이터를 소비할 수 있다.

### Capacity Modes

- Provisioned Mode
  - 프로비저닝할 샤드 수를 정해서 수동으로 확장
  - 샤드를 프로비저닝할 때마다 시간당 비용 부과
- On-Demand Mode
  - 샤드를 프로비저닝하지 않고 필요할 때마다 자동으로 확장

### Kinesis Data Streams Security

- IAM 정책을 사용하여 샤드 생성 및 샤드를 읽어들이는 접근 권한을 제어
- HTTPS 전송 중 암호화
- 클라이언트측 암호화

<br>
<br>
<br>

## Kinesis Data Firehose

- 생산자로부터 데이터를 쉽해서 S3, Amazon Redshift, Amazon Elasticsearch Service 같은 서비스로 쉽게 전달 가능한 완전 관리형 서비스
- 관리가 필요하지 않음
- 자동으로 용량 크기 조정
- Firehose를 통하는 데이터에 대해서만 비용 지불
- Near Real Time

## SQS, SNS, Kinesis

- SQS
  - 컨슈머가 대기열에서 데이터를 pull 하는 모델
  - 데이터 처리 후 컨슈머가 대기열에서 삭제해서 다른 컨슈머가 읽을 수 없도록 해야 함.
  - 관리형 서비스 이므로 처리량을 프로비저닝 할 필요가 없다.
- SNS
  - 게시/구독 모델로 다수의 구독자에게 데이터를 push 하는 모델
  - 주제별 1250만명의 구독자 까지 가능
  - 데이터가 한번 snㄴ에 전송되면 지속되지 않는다.(잃어버릴 수 있음)
  - 처리량 프로비저닝 안해도 됨
- Kinesis
  - 컨슈머가 kinesis에서 데이터를 pull 하는 모델
    - 샤드당 2mb/s의 속도 지원
  - 팬아웃 유형의 소비 매커니즘
    - kinesis가 컨슈머에게 push
    - 샤드 하나에 소비자당 2mb/s 속도
