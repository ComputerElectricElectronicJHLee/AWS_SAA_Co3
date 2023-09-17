# AWS_SAA_Co3
리전은 데이터 센터의 집합

리전은 법률 준수, 지연 시간, 모든 리전이 모든 서비스를 가지고 있지 않음, 요금

AZ(가용영역)은 리전 내 여러 개 존재

각각의 AZ는 여분의 전원, 네트워킹 그리고 통신 기능을 갖춘 하나 또는 두 개의 개별적인 데이터 센터로 이루어짐

각각의 AZ들이 재난 발생에 대비해 서로 분리됨

이러한 AZ와 데이터센터들은 높은 대역폭의 초저지연 네트워킹으로 서로 연결되어 리전을 형성

[IAM(Identity and Access Management)]
- 글로벌 서비스
- 사용자 생성하고 그룹에 배치
- 계정 생성 시 루트 계정 생성
- 루트 계정은 계정(사용자) 생성시에만 사용
- 하나의 사용자는 조직 내의 한 사람에 해당
- 그룹에는 사용자만 배치 가능, 다른 그룹 포함 불가능
- 한 사용자가 다수의 그룹 가능
- 그룹을 형성하는 이유는 AWS 계정을 사용하도록 허용하기 위해
- 그리고 허용을 위해 권한 부여를 해야됨
- 이를 위해 사용자 또는 그룹에게 정책 또는 IAM 정책이라고 불리는 JSON 문서 지정 가능
- 비용 절감 및 보안을 위해 최소 권한 원칙 적용

[IAM 정책]
- inline 정책 : 그룹이 아닌 사용자에게 직접 정책 적용
- 정책구조 : Version, ID(Optional), Statement(내용)
- Statement 구성요소
1. Sid(문장 식별자, Optional)
2. Effect(접근 허용 or 거부)
3. Principal(특정 정책이 적용될 사용자/계정/혹은 역할로 구성)
4. Action(Effcect에 기반해 허용 및 거부되는 API 호출 목록)
5. Resource(적용될 Action의 리소스 목록)
6. Condition(Statement가 언제 적용될지 결정, Optional)

[IAM 비밀번호 정책]
1. 비밀번호 최소 길이 설정
2. 특정 유형의 글자 사용 요구
3. IAM사용자들의 비밀번호 변경 허용 및 금지
4. 일정기간이 지나면 새비밀번호 설정
5. 비밀번호의 재사용을 막음

[IAM MFA(Multi Factor Authentication)]
- 다요소 인증
- 필수적으로 사용하도록 권장
- 루트 계정은 구성 변경 및 리소스를 삭제할 수 있으므로 반드시 보호해야 함
- MFA = 비밀번호 + 보안 장치(MFA 장치)
- MFA 장치 종류
1. 가상 MFA 장치(ex. Google Authenticator, Authy 등)
2. U2F 보안키(Universal 2nd Factor, ex.Yubikey)
3. 하드웨어 Key Fob MFA Device(ex. Gemalto, SurePassID(AWS GovCloud 사용 시))

[AWS 접속 방법]
- AWS Management Console
1. Password
2. MFA
- CLI(Command Line Interface)
- SDK(Software Develope Kit)

[AWS Access 키]
- 터미널에서의 AWS 엑세스를 가능하게 함
- 관리 콘솔을 사용해서 생성 가능
- 사용자들이 자신들의 엑세스 키를 직접 관리
- 비밀번호와 동일한 취급
- Access Key ID ~= username
- Secret Access Key ~= password

[CLI]
- 명령줄 인터페이스
- 엑세스 키에 의해 보호됨
- AWS 서비스의 공용 API로 직접 액세스가 가능
- CLI를 통해 리소스를 관리하는 스크립트를 개발하여 일부 작업 자동화 가능
- AWS 관리 콘솔 대신 사용되기도 함

[SDK]
- AWS로부터 애플리케이션 코드 내에서 API를 호출하고자 할 때 사용되는 방식
- CLI와 동일한 엑세스 키에 의해 보호됨
- 특정 언어로 된 라이브러리의 집합
- AWS 서비스나 API에 프로그래밍을 위한 액세스가 가능하도록 해줌
- 터미널에서 사용하는 것이 아닌 코딩을 통해 애플리케이션 내에 심어두어야 함

[IAM ROLE]
- AWS Service에 권한 부여
- 사용자와 같지만 실제 사람이 사용하도록 만들어진 것이 아니고 AWS 서비스에 의해 사용되도록 만들어짐

[IAM 보안도구]
- IAM Credentials Report(account-level) : IAM 자격 증명 보고서
1. 계정에 있는 사용자와 다양한 자격 증명의 상태를 포함
- IAM Access Advisor(user-level)
1. 사용자에게 부여된 서비스의 권한과 해당 서비스에 마지막으로 엑세스한 시간이 보임
2. 최소 권한 원칙으로 설정할 때 매우 도움되는 정보

[EC2, Elastic Compute Cloud]
- 가장 인기있는 서비스
- 서비스형 InfraStructure
- EC2는 하나의 서비스가 아님
- 가상 머신을 EC2에서 임대할 수 있는데 이를 EC2 인스턴스라고 함
- 데이터를 가상 드라이브 또는 EBS 볼륨에 저장
- ELB(Elastic Load Balancer)로 로드 분산
- ASG(Auto Scaling Group)를 통해 서비스를 확장
- 핵심은 원하는 대로 가상 머신을 선택하여 AWS에서 빌릴 수 있음

[EC2 인스턴스 운영체제 선택]
- EC2 인스턴스의 운영 체제로 리눅스(가장 인기있음), 윈도우, 맥OS 선택 가능
- CPU 개수
- RAM(Random Access Memory)의 양- 저장용량
1. 네트워크를 통해 연결한 스토리지가 필요한 경우 EBS, EFS
2. 하드웨어에 연결할 경우 EC2 인스턴스 스토어가 됨
- EC2 인스턴스에 연결할 네트워크 종류 선택
1. 속도가 빠른 네트워크 카드인지
2. 어떤 종류의 공용 IP를 원하는지
- EC2 인스턴스의 방화벽 규칙 선택(보안 그룹)
- 인스턴스를 구성하기 위한 부트스트랩 스크립트(처음에 설정하는 EC2 사용자 데이터)

[EC2 User Data]
- EC2 사용자 데이터 스크립트를 사용하여 인스턴스를 부트스트래핑 가능
- 부트스트래핑은 머신이 작동될 때 명령을 시작하는 것, 즉 부팅 작업을 자동화
1. 업데이트
2. 소프트웨어 설치
3. 일반 파일 인터넷에서 다운로드 등
- 즉 스크립트는 처음 시작할 때 한 번만 실행되고 다시 실행되지 않음
- 사용자 데이터 스크립트에 작업을 더 추가할 수 록 부팅 시 인스턴스가 할 일 증가
- EC2 사용자 데이터 스크립트는 루트 계정에서 실행되므로 모든 명령문은 sudo로 해야됨
