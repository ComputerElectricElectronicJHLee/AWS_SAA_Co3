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

[AWS 인스턴스 명명 규칙]
- m5.2xlarge(=범용 인스턴스 5세대)
1. m : 인스턴스 클래스
2. 5 : 인스턴스 세대
3. 2xlarge : 인스턴스의 크기

[인스턴스 유형]
- General Purpose(범용 인스턴스)
1. 웹 서버, 코드 Repository 등 다양한 작업에 적합
2. 컴퓨팅, 메모리, 네트워킹 간의 균형도 잘맞음
3. ex) t2.micro

- Compute Optimized(컴퓨팅 최적화 인스턴스)
1. 컴퓨터 집약적인 작업에 최적화된 인스턴스(고성능 프로세서)
2. 고성능 CPU와 컴퓨팅이 요구되는 작업에 사용
ex 1. 일부 데이터를 일괄 처리에 사용 
ex 2. 미디어 트랜스코딩 작업 시
ex 3. 고성능 웹서버가 필요하거나 
ex 4. 고성능 컴퓨팅(HPC) 작업을 할때
ex 5. 머신 러닝이나 
ex 6. 전용 게임 서버가 있을 때 사용
3. 이름이 C로 시작

- Memory Optimized(메모리 최적화 인스턴스)
1. 메모리(RAM)에서 대규모 데이터 셋을 처리하는 유형의 작업에 빠른 성능을 제공
2. 고성능 관계형 or 비관계형 DB 사용
ex 1. Elastic Cash
ex 2. 분산 web scale cach 저장소
ex 3. BI(비즈니스 인텔리전스)에 최적화된 In-메모리 DB
ex 4. 대규모 비정형 데이터의 실시간 처리를 실행하는 애플리케이션에 사용
3. 이름이 R로 시작하지만 X1이나 Z1도 있음

- Storage Optimized(스토리지 최적화 인스턴스)
1. 로컬 스토리지에서 대규모의 데이터셋에 access할 때 적합
ex 1. OLTP(고주파 온라인 트랜잭션 프로세스) 시스템
ex 2. 관계형 DB or 비관계형 DB(NoSQL)에 사용
ex 3. 메모리 DB의 캐시(~= Redis)
ex 4. 데이터 웨어하우징 애플리케이션
ex 5. 분산 파일 시스템
2. 이름이 I, G 또는 H1으로 시작

[보안 그룹(방화벽)]
- EC2 인스턴스에 들어오고 나가는 트래픽을 제어
- 허용 규칙만 포함
- 출입이 허용된 것이 무엇인지 확인 가능
- IP주소를 참조하여 규칙 생성 가능
(컴퓨터의 위치나 다른 보안 그룹을 참조하는 것)
- 보안 그룹끼리 서로 참조 가능

[보안 그룹 예시]
- 컴퓨터에서 공공 인터넷을 사용하여 EC2 인스턴스를 엑세스하는 상황
- 보안 그룹은 외부에서 EC2 인스턴스로 들어오는 것(인바운드 트래픽)이 허용되면 아웃바운드 트래픽도 수행 가능
1. 보안 그룹은 EC2 인스턴스의 방화벽이며 포트로의 엑세스를 통제
2. 인증된 IP 주소의 범위를 확인하여 IPv4인지 Ipv6인지 확인
3. 외부에서 인스턴스로 들어오는 인바운드 네트워크 통제
4. 인스턴스에서 외부로 나가는 아웃바운드 네트워크도 통제

[보안그룹]
- 인바운드 규칙
1. 권한 없는 IP의 컴퓨터가 EC2 인스턴스에 엑세스하려고 하면 방화벽이 차단하여 타임아웃 발생
2. 모든 인바운드 트래픽 차단
- 아웃바운드 규칙
1. 모든 보안 그룹의 EC2 인스턴스는 기본적으로 모든 트래픽 허용
2. EC2 인스턴스가 웹사이트에 엑세스하고 연결을 시도하면 보안 그룹에서 허용
- 보안 그룹과  인스턴스는 M:N 관계
- 보안 그룹은 리전과 VPC 결합으로 통제
- 리전 전환 시 새 보안그룹 생성하거나 다른 VPC 생성해야 됨
- 보안그룹은 EC2 외부에 있어서 트래픽이 차단되면 EC2 인스턴스는 방화벽을 확인 불가능
- SSH 엑세스를 위해 하나의 별도 보안 그룹을 유지
- 타임아웃, 대기, 멈춤은 보안 그룹 문제
- 연결 거부 응답을 받았으면 보안그룹은 실행되었고 트래픽 통과했지만 애플리케이션에 문제가 생김
- 로드 밸런서를 사용한 보안그룹
1. 보안 그룹1이 보안 그룹2에 인바운드를 허용
2. 보안 그룹2에 연결된 어떤 인스턴스도 바로 통신이 가능
3. 이는 IP를 신경쓰지 않아도 되게 함

[SSH]
- 22 = SSH (Secure Shell) - log into a Linux instance
- 22번 포트로 Linux에서 EC2 인스턴스로 로그인하도록 함
- 21 = FTP (File Transfer Protocol) - upload file into a file share
- SSH를 사용해서 업로드하고 보안 파일 전송 프로토콜이 되기 때문에 SSH가 22번 포트를 사용
- 80 = HTTP - access unsecured websites
- 443 = HTTPS - access secured websites
- 3389 = RDP (Remote Desktop Protocal) - log into a Windows instance

[SSH]
- 클라우스에서 실행 시 유지 보수나 조치를 취하기 위해 서버 내부와 연결해야됨
- Linux 서버에서는 시큐어 셸인 SSH를 서버에 사용
- SSH는 명령줄 인터페이스 도구로 Mac, Linux, 윈도우10 이상에서 사용가능
- 윈도우 10미만은 putty사용
- EC2 Instance Connect는 터미널, putty가 아닌 웹 브라우저로 EC2 인스턴스에 연결

[EC2 인스턴스 구매 옵션]
- On-Demand 인스턴스
1. 단기적인 워크로드
2. 비용 예측가능
3. 초 단위 요금(가장 비쌈)
4. 단기적으로 중단없는 워크로드가 필요할 때 or 애플리케이션의 거동을 예측할 수 없을떄

- 예약 인스턴스
1. 기간은 1년 or 3년
2. 장기간의 워크로드가 target
3. 특정한 인스턴스 속성(인스턴스 타입, 리전, OS 등) 예약

- 전환형 예약 인스턴스
1. 시간이 지나면 인스턴스 타입, OS 등이 변경

- 절약 플랜
1. 기간은 1년 or 3년
2. 달러 단위로 특정한 사용량을 약정
3. 장기 워크로드를 위함
4. 특정한 인스턴스 패밀리, 리전으로 고정됨
5. 인스턴스 사이즈, OS, Tenancy 전환 가능

- Spot 인스턴스
1. 아주 짧은 워크로드를 위함
2. 아주 저렴함
3. 최대 가격 정의 후 스폿 가격이 최대 가격을 넘게 되면 인스턴스 손실
4. 신뢰성이 낮음
5. 고장에 대한 회복력이 있는 인스턴스라면 아주 유용
6. 아주 중요한 작업이나 데이터베이스는 적절하지 않음
ex) 배치, 데이터 분석, 이미지 처리, 모든 종류의 분산형 워크로드, 시작 및 종료 시간이 유연한 워크로드

- 전용 호스트
1. 물리적 서버 전체를 예약해서 인스턴스 배치를 제어할 수 있음
2. 온디맨드 or 1년 예약 or 3년 예약
3. 물리적 서버를 예약하므로 가장 비싼 옵션
4. 물리적 서버 자체에 대한 접근성을 갖고 낮은 수준의 하드웨어에 대한 가시성을 제공
ex) 법규 준수 요건이 있거나 소켓, 코어 VM 소프트웨어 라이센스를 기준으로 청구되는 기존의 서버에 연결된 SW 라이센스

- 전용 인스턴스
1. 다른 고객이 여러분의 하드웨어를 공유하지 않는다는 의미
2. 고객의 전용 하드웨어에서 실행되는 인스턴스
3. 고객은 같은 계정에서 다른 인스턴스와 함께 하드웨어를 공유할 수 있고 인스턴스 배치에 대한 통제권이 없음
4. 자신만의 인스턴스, 자신만의 하드웨어를 가짐

- 용량 예약
1. 원하는 기간동안 특정한 AZ에 온디맨드 인스턴스를 예약할 수 있음
2. 기간 약정 없이 언제라도 용량 예약 및 취소 가능
3. 청구 할인을 위해 지역별 예약 인스턴스와 결합하거나 절약 플랜과 결합
4. 인스턴스 실행과 무관하게 온디맨드 요금 부과
5. 특정한 AZ에 있어야 하는 단기적이고 중단 없는 워크로드에 아주 적합

[EC2 스팟 인스턴스]
- 지불할 수 있는 최대 스팟 가격 정의
- 인스턴스의 스팟 가격이 우리가 지불하고자 하는 최대 가격보다 낮다면 해당 인스턴스 유지
- 시간당 스팟은 offer와 용량에 따라 달라짐
- 현재 스팟 가격이 정의된 최대 가격을 초과하면 두 가지 선택 가능(2분의 유예 기간 주어짐)
1. 하던 작업을 모두 중지하고 인스턴스를 중지 => 스팟 가격이 최대 가격 아래로 다시 내려가면 인스턴스 재시작하고 중단했던 곳부터 재개
2. EC2 인스턴스 종료 => 작업을 다시 시작할 때 새로운 EC2 인스턴스로 시작
- AWS가 스팟 인스턴스 회수하는 것을 원하지 않는다면 스팟 블록 사용가능
1. 지정된 기간동안 스팟 인스턴스를 차단
2. 1~6시간 가능
3. 그동안 중단 없이 해당 블록을 사용할 수 있다고 규정
4. 아주 드물게 인스턴스가 회수되는 경우가 있음
5. 스팟 가격은 AZ에 따라 달라짐

[스팟 인스턴스 종료하는법]
- 스팟 요청에서는 원하는 인스턴스 수, 최대 가격 및 시작 사양 등을 정의
- 언제부터 언제까지 유효한지, 무한대도 가능
- 요청 유형
1. 스팟 인스턴스 일회성 요청
a. 스팟 요청이 완료되는 즉시 인스턴스가 시작
b. 스팟 요청이 사라짐
2. 영구 인스턴스 요청
a. 스팟 요청이 유효한 기간 동안은 이 인스턴스 수도 유효
b. 인스턴스가 어떤 이유로든 중지되거나 스팟 가격을 기준으로 중단되는 경우 스팟 요청이 다시 실행되고 유효성이 확인되면 스팟인스턴스가 자동으로 다시 시작
- 스팟 요청을 취소하려면 Open, Active, Disabled 상태여야 함(failed, canceled 상태에서는 안됨)
- 스팟 요청을 취소하고 싶을 때는 이전에 시작한 인스턴스를 종료하는 것이 아님(인스턴스를 종료하는 것은 AWS가 아닌 고객이 할일이므로)
- 스팟 인스턴스를 완전히 종료하기 위해 스팟 요청을 취소하고 그 다음 관련 스팟 인스턴스를 종료해야 함(다시 시작안되도록)

[스팟 Fleets]
- 비용을 절감하는 궁극적인 방법
- 스팟 인스턴스 세트를 정의하는 방법(+(Optional) 온디맨드 인스턴스)
- 스팟 플릿은 정의한 가격 제한으로 목표 용량을 충족시키기 위해 최선을 다함
1. 가능한 launch pools : 다양한 인스턴스 타입, OS, AZ
2. 스팟 플릿이 가장 적합한 launch pool을 선택
- 스팟 플릿이 예산에 도달하거나 원하는 용량에 도달하면 launch 인스턴스를 중지
- 따라서 스팟 플릿에 스팟 인스턴스를 할당하는 전략을 정의해야 함
1. 최저 가격
a. 스팟 플릿은 가장 낮은 가격인 pool에서 인스턴스를 시작하기 때문에 비용이 최적화
b. 워크로드가 매우 짧은 경우 좋은 옵션
2. 다양한 방법으로 스팟 인스턴스 실행
a. 스팟 인스턴스는 모든 pool에 분산
b. 가용성과 긴 워크로드에 적합
c. 한 pool이 사라져도 다른 pool은 여전히 활성화
3. 용량 최적화
a. 원하는 인스턴스 수에 맞는 최적의 용량을 가진 pool을 갖게 됨
4. 가격 용량 최적화
a. 먼저 사용 가능한 용량이 가장 큰 pool을 선택하고 그 중 가격이 가장 낮은 pool을 선택하는 전략
b. 대부분의 워크로드에 가장 적합한 선택
- 스팟 플릿을 사용하면 여러 개의 Launch pool과 여러 인스턴스 타입을 정의할 수 있어 전력만 신경쓰면 됨
- 스팟 플릿에서 최저가 할일 또는 최저가 전략을 사용하면 스팟 플릿이 자동으로 가장 낮은 가격의 스팟 인스턴스를 요청
- 스팟 플릿은 스팟 인스턴스를 기반으로 추가 비용 절감

[스팟 인스턴스 vs 스팟 플릿]
- 간단한 스팟 인스턴스를 요청하는 경우는 원하는 인스턴스 유형과 AZ를 정확히 알고 있는 경우
- 스팟 플릿을 요청하는 경우는 조건에 만족하는 모든 인스턴스 유형과 모든 AZ를 선택

[Private vs Public vs Elastic IP]
- IPv4
1. 가장 대중적인 IP
2. 네 개의 숫자가 세 개의 점으로 분리된 형태
3. [0-255].[0-255].[0-255].[0-255]
ex) 1.160.10.240
- IPv6
1. 조금 덜 대중적임
2. 정말 길고 독특한 숫자 기호와 문자로 이루어짐
ex) 1900:4545:3:200:f8ff:fe21:67cf
- Public IP
1. 인터넷 전역에 엑세스 가능
2. Public IP를 가진 서버들끼리 IP를 사용하여 서로 통신 가능
3. 기기가 인터넷상에서 식별될 수 있음을 의미(ex. WWW)
4. 공용IP가 전체 웹에서 유일한 것이어야 함
5. IP의 지리적 위치를 쉽게 찾을 수 있음

- Private IP
1. Private 네트워크 내에서만 엑세스 가능
2. Private 네트워크에는 사설 IP 범위가 있는데 기본적으로 Private 네트워크 내의 모든 컴퓨터가 사설 IP를 사용하여 서로 통신할 수 있음
3. public 게이트웨이인 인터넷 게이트웨이(+NAT 장치)를 이용하면 다른 서버에 엑세스 가능
4. 기기가 Private 네트워크 안에서만 식별 가능
5. IP가 Private 네트워크 안에서만 유일하면 됨
6. 지정된 범위의 IP만 사설 IP로 사용 가능

- Elastic IP
1. EC2 인스턴스를 시작하고 중지할 때 공용IP를 바꿀 수 있음
2. 인스턴스에 고정된 IP를 사용하면 Elastic IP가 필요
3. Elastic IP는 Public IP
4. 삭제되지 않는 한 계속 가지고 있음
5. 한 번에 한 인스턴스에만 attach 가능
6. 계정당 탄력적 IP를 5개만 사용 가능(AWS에 개수 증가를 요청할 수 있지만 드문 케이스)
6-1. 위로 인해 IP 주소가 탄력적이면 한 인스턴스에서 다른 인스턴스로 빠르게 이동함으로써 인스턴스 또는 소프트웨어의 오류를 마스킹할 때 사용할 수 있는 경우가 드뭄
7. 매우 좋지 않은 구조적 결정으로 탄력적 IP는 사용하지 않는 것이 좋음
8. 대신 임의의 공용 IP를 써서 DNS 이름을 할당하는 것이 좋음
9. DNS는 Route53에서 살펴볼 예정으로 훨씬 더 많은 제어가 가능하고 확장 가능성이 큼
10. 로드 밸런서를 사용해서 공용IP를 전혀 사용하지 않을 수 도 있음
11. 9와 10이 AWS에서 취할 수 있는 최상의 패턴

- EC2 기기에 SSH를 할 땐 VPN을 쓰지 않는 이상 같은 네트워크가 아니므로 Private IP 사용 불가능
- 기기를 멈췄다가 다시 시작하면 공용IP가 바뀔 수 있음

[EC2 배치 그룹]
- EC2 인스턴스가 AWS 인프라에 배치되는 방식을 제어할 때 사용
- AWS의 하드웨어와 직접적인 상호 작용을 하지는 않지만 EC2 인스턴스가 각각 어떻게 배치되기를 원하는지 AWS에 알려줌
- 배치 그룹을 만들 때 세 가지 전략 사용 가능

1. Cluster - 클러스터 배치 그룹
a) 단일 AZ 내에서 지연 시간이 짧은 하드웨어 설정으로 인스턴스를 그룹화 할 클러스터 배치 그룹
b) 모든 인스턴스가 동일한 Rack에 있음 즉 동일한 하드웨어와 동일한 AZ에 있다는 거임
c) 지연시간이 매우 짧은 10GB속도의 높은 성능 제공
d) Rack에서 Fail이 발생 즉 하드웨어에 Fail이 발생하면 모든 EC2 인스턴스가 동시에 Fail하므로 위험도 높음
e) 극히 짧은 지연 시간과 높은 네트워크 처리량을 필요로 하는 애플리케이션에 적용 가능(ex. 빅데이터)

2. Spread - 분산 배치 그룹
a) 모든 EC2 인스턴스를 다른 하드웨어에 분산하여 Fail 위험 최소화
b) 배치 그룹의 AZ 당 7개의 EC2 인스턴스만 가질 수 있다는 제한 사항있음
c) 위와 같이 배치 규모에 제한이 있어 크기는 적당하지만 너무 크지는 않은 애플리케이션에서만 쓸 수 있음
d) 가용성을 극대화하고 위험을 줄여야하는 크리티컬한 애플리케이션이 있는 경우 분산 배치 그룹 사용

3. Partition - 분할 배치 그룹(매우 유용함)
a) 분산 배치 그룹과 비슷하게 인스턴스를 분산하려는 것
b) 여러 파티션에 인스턴스가 분할되어 있고 이 파티션은 AZ내의 다양한 하드웨어 Rack 세트에 의존
c) 가용 영역 당 최대 7개의 파티션이 있을 수 있음(각 파티션은 AWS Rack을 의미)
d) 파티션이 많으면 인스턴스가 여러 하드웨어 Rack에 분산되어 서로 Rack Fail로부터 안전
e) 파티션은 동일한 리전의 여러 AZ영역에 걸쳐 있을 수 있음
f) 설정으로 최대 수백 개 EC2 인스턴스를 얻을 수 있음
g) EC2 인스턴스가 어떤 파티션에 있는지 알기 위해 메타데이터 서비스를 사용하여 이 정보에 엑세스하는 옵션이 있음
h) 파티션들 전반에 걸쳐 데이터와 서버를 퍼트려 두도록 파티션 인식 가능한 애플리케이션에 사용
i)그룹 당 수백 개의 EC2 인스턴스를 통해 확장가능하고 이를 통해 하둡, Cassandra, Kafka 같이 파티션을 인식하는 빅데이터 애플리케이션에 사용

[Elastic Network Interface(ENI)]
- VPC의 논리적 구성 요소이며 가상 네트워크 카드를 나타냄
- EC2 인스턴스가 네트워크에 엑세스할 수 있게 해줌
- ENI는 EC2 인스턴스 외부에서도 사용됨
- 주요 사설 IPv4와 하나 이상의 보조 IPv4를 가질 수 있음 즉 EC2에 보조 ENI를 얼마든지 추가 가능
- 각 ENI는 사설 IPv4당 탄력적 IPv4를 갖거나 하나의 공용 IPv4를 가질 수 있으므로 사설 및 공용 IP가 한 개씩 제공됨
- ENI에 하나 이상의 보안 그룹을 연결할 수 있음
- Mac 주소 및 기타 항목을 연결할 수 있음
- EC2 인스턴스와 독립적으로 ENI를 생성하고 즉시 연결하거나 장애 조치를 위해 EC2 인스턴스에서 이동시킬 수 있음
- ENI는 특정 AZ에 바인딩됨 즉 특정 AZ에서 ENI를 생성하면 해당 AZ에만 바인딩 가능
- 첫 번째 EC2 인스턴에서 두 번째 EC2 인스턴스로 ENI를 옮겨서 사설 IP를 이동시킬 수 있음
- 그러면 사설 IP가 첫 번쨰 문제 인스턴스에서 두 번째 EC2 인스턴스로 연결됨 이는 장애 조치에 매우 유용

[EC2 절전모드(Hibernate)]
- 인스턴스를 중지하면 EBS 디스크 데이터는 다시 시작할 때까지 그대로 유지
- 인스턴스를 종료한다면 root 볼륨(EBS)이 삭제되게 했다면 인스턴스도 삭제
- 그렇게 설정하지 않은 다른 볼륨은 인스턴스가 종료되더라도 그대로 남음
- 인스턴스를 다시 시작하면 운영체제가 먼저 부팅되기 시작하고 EC2 사용자 데이터 스크립트도 실행됨
- 그 뒤 운영체제 부팅이 완료되고 애플리케이션도 실행되며 캐시도 구성되기 시작하므로 과정이 끝날 때까지 시간이 다소 걸림
- 인스턴스가 절전 모드가 되면 RAM에 있던 인 메모리 상태는 그대로 보존되어 인스턴스 부팅이 더 빨라짐
- 운영체제를 완전히 중지하거나 다시 시작하지 않고 그대로 멈췄기때문임
- 절전모드가 되고 백그라운드에서 RAM에 기록되었던 인 메모리 상태는 루트 경로의 EBS 볼륨에 기록되기 때문에 루드 EBS 볼륨을 암호화해야 함
- 볼륨 용량도 RAM을 저장하기에 충분해야함
- 인스턴스를 다시 실행하면 디스크에서 RAM을 불러와 EC2 인스턴스 메모리로 가져옴
- EC2 인스턴스를 중지한 적 없는 것처럼 됨
- 지원하는 제품군이 많고 인스턴스 RAM 크기는 최대 150GB
- 베어 메탈 인스턴스에 적용할 수 없고 Linux, Windows 등의 여러 운영 체제에서 사용할 수 있음
- 루트 볼륨, 즉 EBS에만 저장이 가능하며 암호화가 필요하고 덤프된 RAM을 포함할만큼 충분한 용량이 있어야 함
- 온디맨드, 예약, 스팟과 같은 모든 종류의 인스턴스에 사용 가능
- 절전 모드는 최대 60일까지 사용 가능

[EC2 Hibernate 사용 사례]
- 오래 실행되는 프로세스를 갖고 있고 중지하지 않을 때
- RAM 상태를 저장하고 싶을 때
- 빠르게 재부팅을 하고 싶을 때
- 서비스 초기화가 시간을 많이 잡아먹어 서비스가 중단없이 인스턴스를 절전 모드로 전환하고 싶을 때

[Elastic Block Store(EBS)]
- 인스턴스가 실행 중인 동안 연결가능한 네트워크 드라이브(물리적 드라이브가 아님)
- EBS 볼륨을 사용하면 인스턴스가 종료된 후에도 데이터를 지속할 수 있음
- 인스턴스를 재생성하고 이전 EBS 볼륨을 마운트하면 데이터를 다시 받을 수 있음
- CCP 레벨의 EBS 볼륨은 한 번에 하나의 인스턴스에만 마운트 가능 / 일부 EBS는 다중 연결(인스턴스 하나에 여러 개 EBS 볼륨 연결은 가능)
- EBS 볼륨을 생성할 때는 특정 AZ 영역에서만 사용 가능
- us-east-1a에서 생성된 경우 us-east-1b에는 연결 불가능
- 스냅샷을 이용하면 다른 AZ으로도 볼륨을 옮길 수 있음
- EBS 볼륨은 네트워크 UBS 스틱과 유사함
- UBS 스틱처럼 한 컴퓨터에서 꺼내서 다른 컴퓨터에 꽂는 장치는 맞지만 실제 물리적 연결이 아닌 네트워크를 통해 연결
- 무료 등급으로는 매달 30GB의 EBS 스토리지를 범용 SSD or 마그네틱 유형으로 제공
- 인스턴스와 EBS 볼륨이 서로 통신을 하기 위해 네트워크를 필요
- 네트워크가 사용되기 때문에 컴퓨터가 다른 서버에 도달할 때 지연이 생길 수 있음
- EBS 볼륨은 네트워크 드라이브이므로 EC2 인스턴스에서 분리될 수 있고 매우 빠르게 다른 인스턴스로 연결 가능
- 이로 인해 대체 작동 등의 경우에 매우 유용
- 볼륨이기 때문에 용량을 미리 결정해야 하므로 원하는 양의 GB 및 IOPS, 즉 단위 초당 전송 수를 미리 지정해야함(향후에 용량을 늘릴 수 있음)
- 해당 프로비전 용량에 따라 요금이 청구됨

[인스턴스 종료 시 EBS 삭제]
- EC2 인스턴스를 통해 EBS 볼륨을 생성하는 경우 종료 시 삭제 속성이 있음
- 기본 설정으로는 루트 볼륨에 체크되어 있고 새로운 EBS 볼륨에는 체크되어있지 않음
- 인스턴스가 종료될 때 루트 볼륨을 유지하고자 하는 경우, 데이터를 저장하고자 하는 등의 경우에는 루트 볼륨의 종료 시 삭제 속성을 비활성화하면 됨
