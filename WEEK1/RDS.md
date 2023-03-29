# AWS RDS(Relational Database Service)

- aws rds는 관계형 데이터베이스를 관리해주는 서비스이다.
- aws rds에서 사용 가능한 db 종류
  - PostgreSQL
  - MySQL
  - MariaDB
  - Oracle
  - Microsoft SQL Server
  - Aurora
- rds가 제공하는 기능
  - Automated Provisioning, OS Patching
  - 지속적인 백업 및 특정 시점으로 복원 가능
  - 대시보드 모니터링 제공
  - 읽기 전용 레플리카를 활용해 읽기 성능 향상
  - 재해복구 목적으로 다중 AZ 설정 가능
  - 수직,수평 확장

## RDS Storage Auto Scaling

- 설정 용량보다 많이 사용하게 되면 rds가 감지해서 자동으로 스토리지를 확장해준다.
- 오토스케일링을 위해 Maximum Storage Threshold를 설정해야 한다.(무한으로 늘어나면 안되기 때문)

## RDS Read Replicas for read scalability(읽기 전용 복제본과 다중az)

- read replica를 생성할때 within az, cross az, cross region으로 생성할 수 있다.
- read replica는 select만 가능, insert, update, delete 불가능

## RDS Read Replicas - Network Cost

- rds read replica의 데이터를 옮길때 같은 리전 안에 다른 az이면 이전 비용 발생 안함
- 근데 다른 리전에 레플리카가 있으면 네트워크 비용 발생

## RDS Multi-AZ(Disaster Recovery)

- 다중 az는 주로 재해복구에 사용됨
- 마스터 db의 모든 변경사항을 동기적으로 스탠바이 db에 복제해놓고 재해가 발생하면 스탠바이 db를 마스터 db로 승격시키는 방식
- 시험에서 single-aza 에서 multi-az로 변경 가능한지 물어보는데
  - downtime이 발생하지 않고 가능하다.
  - 수정 한번으로 활성화 하면 된다. 이를 통해 마스터db는 동기식 레플리카인 스탠바이 db를 갖게된다.
  - 내부적으로 rds가 자동적으로 마스터db를 스냅샷해서 스탠바이 db에 복원하고 스탠바이가 복원되면 마스터와 스탠바이간에 동기화가 설정되므로 스탠바이db가 마스터db의 내용을 수용하므로 다중az 설정이 된다.

## RDS Custom

- rds custom은 oracle과 mssql에서만 사용 가능
- 기저 db와 os에 대한 권한 전체를 갖게 됨.(그냥 rds는 aws가 알아서 관리 함)

<br >
<br >
<br >
