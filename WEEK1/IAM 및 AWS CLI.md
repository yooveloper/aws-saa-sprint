# IAM(Identity and Access Management)

aws 를 사용하는 계정을 생성하고 권한을 부여하는 서비스

최초 aws 서비스에 가입할때 생기는 계정은 root 권한 계정임

모든 서비스는 root 계정에서 생성한 하위 계정으로 작업하는게 좋음

- 사용자를 생성하고 권한을 부여하기 때문에 global service 임
- Root 계정은 사용자를 생성할때만 사용해야 하고 다른 용도로는 사용x
- 계정 1 개 === 1명의 사람, 원하면 그룹으로 묶을수도 있음
- 하나의 계정은 여러 그룹에 속할수도 있음

<br >

## 계정 보안 관련

사용자 계정의 보안을 강화하기 위한 방법들

- 비밀번호 생성 정책
- iam 유저들에게 비밀번호를 못 바꾸게 함
- 일정기간이 지나면 비밀번호를 바꾸도록 하게 함
  - 이전에 사용한 비밀번호는 재설정 못하게

<br >

### MFA(Muilti Factor Authentification)

- AWS 에서 필수적으로 적용해야 하는 보안 정책
- 특히 root 계정은 무조건 해야 하고 iam 계정도 해야 함.
- 쉽게 말하면 기존에 알고 있는 비밀번호 + 다른 디바이스의 인증방법으로 로그인 하는것
- AWS에서 사용하는 MFA 장치

  1. Virtual MFA
     1. Google Authenticator(하나의 폰에서만 가능)
     2. Authy(여러 디바이스에서 가능)
  2. Universal 2nd Factor(U2F)
     1. 물리적인 usb형태의 key로 aws에서 서비스하는 Yubikey가 있음
     2. root를 비롯한 여러 iam 계정 사용 가능
  3. Hardware Key-Fob

  <br >

## 정리

1. 루트 계정을 사용하지 말고 iam으로 사용자 계정을 만들어서 써라
2. 비밀번호 정책을 정하고, MFA를 써라
3. 서비스에 권한을 부여할때마다 역할(Role)을 만들고 사용해라
4. cli/sdk를 사용할 경우 액세스키를 만들어라
5. 계정의 권한을 검사할때는 IAM Credentials Report를 봐라
