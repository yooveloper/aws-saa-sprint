# Amazon EMR(Elastic MapReduce)

Amazon EMR은 Apache Hadoop 및 Apache Spark와 같은 빅 데이터 프레임워크 실행을 간소화하여 방대한 양의 데이터를 처리하고AWS 분석하는 관리형 클러스터 플랫폼

- 빅데이터 작업을 위한 하둡 클러스터 생성에 사용된다.
- 시험에서 하둡 클러스터 관련된 빅데이터 내용 나오면 EMR
- 클러스터는 EC2인스턴스의 모음이고 클러스터 안에서 각각에 인스턴스를 노드라고 함.
- 온디맨드, 예약, 스팟 인스턴스 지원

## EMR Node Types

- 마스터 노드: 클러스터 관리
- 코어 노드: 작업 수행, 데이터 저장
- 작업 노드: 작업을 수행하는 노드