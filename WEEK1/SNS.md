# Amazon SNS

- 게시자에서 구독자로 메시지를 전송하는 관리형 서비스
- 클라이언트는 sns topic을 구독하고 http, email mobile sms, push 등으로 수신 가능
- FIFO를 통한 메시지 순서 보장, 그룹 정의, 중복 방지
- 필터 정책을 통해 메시지 필터링

## 보안

- HTTPS 전송 중 암호화
- KMS 키를 사용한 암호화
- 클라이언트 암호화

## 액세스 제어

- IAM을 통해 SNS 액세스 제어
