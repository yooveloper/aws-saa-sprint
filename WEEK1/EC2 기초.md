# EC2(Elastic Compute Cloud)

AWS에서 제공하는 클라우드 컴퓨팅이다.
AWS의 대표적인 서비스, 상품이며 다양한 기능을 제공해준다.

EC2에서 선택 가능한 OS

- Linux, Windows, Mac OS

t2.micro는 free tier이고 한달내내 켜놔도 됨.

public IPv4 address는 EC2인스턴스에 접근하기 위한 주소

private IPv4 address는 aws 네트워크 안에서 EC2 인스턴스에 접근하기 위한 주소

<br >

## EC2 인스턴스 유형

- m: 범용 인스턴스
  - 다양한 작업에 알맞음
  - 컴퓨팅,메모리,네트워크 간의 균형 잘 맞음
- c: 고성능의 CPU를 요구하는 인스턴스
  - 데이터 일괄 처리(배치)
  - 미디어 트랜스코딩 작업
  - 고성능의 웹서버
  - 머신러닝
- r: 메모리 최적화 인스턴스
  - 고성능의 관계형/비관계형 데이터베이스
  - 일라스틱 캐시와 같은 분산 웹스케일 캐시 저장소
  - Business intelligence에 최적화된 인메모리 데이터베이스
  - 대규모 비정형 데이터의 실시간 처리를 실행하는 app

### aws 네이밍 컨벤션의 예

ex) m5.2xlarge

- m: instance class
- 5: generation (AWS improves them over time)
- 2xlarge: size within the instnace class

<br >

## 보안 그룹

- Security Groups 은 EC2인스턴스의 방화벽
- port로의 액세스 통제
- 인증된 IP주소 범위를 확인해 IPv4인지 IPv6인지 확인
- 외부에서 인스턴스로 들어오는 인바운드 네트워크 통제
- 인스턴스에서 외부로 나가는 아웃바운드 네트워크 통제

<br >

## Classic Ports to know

- 22: SSH(Secure Shell) - 리눅스에서 ec2인스턴스로 로그인할때 사용됨.
- 21: FTP(File Transfer Protocol) - 파일 전송 프로토콜의 포트로 사용됨.
- 22: SFTP(Secure File Transfer Protocol) - SSH를 사용한 파일 전송 프로토콜의 포트로 사용됨.
- 80: HTTP - 보안이 되지 않은 웹사이트에 포트로 사용됨.
- 443: HTTPS - 보안이 적용된 웹사이트에 포트로 사용됨.
- 3389: RDP(Remote Desktop Protocol) - 원격 데스크톱 프로토콜의 포트로 사용됨.

<br >

## SSH

- SSH는 명령줄 인터페이스 도구로 Mac,Linux Windows10 이상 에서 사용 가능(윈도우 10 이하버전에서는 putty를 사용)
- SSH는 터미널이나 명령줄을 사용해 원격머신이나 서버를 제어할 수 있게 해줌
- Amazon Linux 2 AMI 에는 ec2-user라는 기본 사용자가 설정되어있음
- ssh로 인스턴스 접속 설정

```shell
$ chmod 400 .pem파일 // pem 파일 권한 설정
$ ssh -i .pem파일 ec2-user@publicIP주소 // 적용
```
