# Amazon Aurora

- aurora는 aws의 클라우드 네이티브 db이고 postgresql과 mysql을 지원한다.
- rds보다 성능이 더 좋다(높은 가용성, 트래픽 처리)
  - 스토리지 용량이 자동으로 증감된다.
  - 데이터를 분산 저장해서 높은 가용성을 가진다.
    - 3개의 az에 6개의 storage 생성
  - 데이터가 손상되면 자동으로 복구함
- 기본적으로 마스터는 1개이며 마스터 외에 read replica를 15개까지 둘 수 있음.
  - 마스터가 문제 생기면 read replica중 하나가 마스터가 됨

## Aurora DB Cluster

- 마스터 db 만을 위한 writer endpoint가 있음.
- reader endpoint가 있어서 클라이언트에서 reader endpoint에 연결될 때마다 자동으로 로드밸런싱 함.

## Aurora Multi-Master

- writer node에 높은 가용성을 확보하고자 할때 사용
- 멀티 마스터 클러스터에 있는 모든 db가 write 가능
