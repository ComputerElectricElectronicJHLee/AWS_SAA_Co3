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

[EBS 스냅샷]
- EBS 볼륨의 특정 시점에 대한 백업
- EBS 인스턴스에서 EBS 볼륨을 분리할 필요는 없지만 권장 사항임
- EBS 스냅샷은 다른 AZ나 다른 리전에도 복사할 수 있음

[EBS 스냅샷 기능]
- EBS 스냅샷 아카이브
1. 최대 75%까지 저렴한 아카이브 티어로 스냅샷을 옮길 수 있는 기능
2. 아카이브를 복원하는 데 24시간에서 최대 72시간이 걸림
3. 즉시 복원되지 않음

- EBS 스냅샷 휴지통
1. EBS 스냅샷을 삭제하는 경우 영구 삭제하는 대신에 휴지통에 넣을 수 있음
2. 실수로 삭제하는 경우에 휴지통에서 복원 가능
3. 휴지통에 보관되는 기간은 1일에서 1년 사이로 설정 가능

- 빠른 스냅샷 복원(FSR)
1. 스냅샷을 완전 초기화해 첫 사용에서의 지연 시간을 없애는 기능
2. 스냅샷이 아주 크고 EBS 볼륨 또는 EC2 인스턴스를 빠르게 초기화해야 할 때 유용
3. 비용이 많이 듬

[Amazon Machine Image(AMI)]
- EC2 인스턴스를 통해 만든 이미지
- AMI로 AWS를 구축할 수 있고 원하는 대로 변경 가능
- AMI에다 원하는 소프트웨어 또는 설정 파일을 추가하거나 별도의 운영 체제를 설치할 수 도 있고 모니터링 툴을 추가할 수 있음
- AMI를 따로 구성하면 부팅 및 설정에 드는 시간을 줄일 수 있음
- EC2 인스턴스에 설치하고자 하는 모든 SW를 AMI가 미리 패키징해줌
- AMI를 특정 리전에 구축한 다음 다른 지역으로 복사해서 AWS의 글로벌 인프라를 활용할 수 있음
- AWS에서 제공하는 AMI, 직접 만든 AMI 등 여러 종류가 있음
- 직접 만든거는 당연하게도 직접 유지 및 관리해야됨
- 다른 사람이 구축한 이미지를 AWS 마켓플레이스 AMI에서 구매하여 EC2 인스턴스를 실행할 수 있음

[AMI Process]
- 먼저 EC2 인스턴스를 원하는 대로 설정해줌
- 그 후 인스턴스를 중지해 데이터 무결성 확보
- 이 인스턴스를 바탕으로 AMI 구축
- 이 과정에서 EBS 스냅샷 생성
- 이 후 다른 AMI에서 인스턴스를 실행할 수 있음

[ECS Instance Store]
- 물리적 서버에 연결된 하드웨어 드라이브
- EC2 인스턴스는 가상 머신이지만 실제로는 하드웨어 서버에 연결되어 있어야함
- 이와 같은 서버에는 해당 서버에 물리적으로 연결된 디스크 공간을 가짐
- EC2 인스턴스 스토어는 I/O 성능 향상을 위해 활용할 수 있음
- 훌륭한 처리량을 갖추고 있어서 월등한 디스크 성능이 필요할 때 EC2 인스턴스 스토어를 확보할 필요가 있음
- EC2 인스턴스 스토어를 중지 또는 종료하면 해당 Storage 또한 손실됨(임시 스토리지)
- 그러므로 EC2 인스턴스 스토어는 장기적으로 데이터를 보관할만한 장소가 될 수 없고 장기 스토리지로는 EBS가 적합
- 버퍼, 캐시, 스크래치 데이터 또는 임시 콘텐츠를 사용하는 경우에 활용
- EC2 인스턴스의 기본 서버에 장애가 발생할 시 해당 EC2 인스턴스가 연결된 하드웨어에도 장애가 발생하므로 데이터 손실에 대한 위험 존재
- 따라서 EC2 인스턴스 스토어를 사용할 때에는 데이터를 백업해 두거나 복제해야함

[EBS 유형]
- gp2/gp3(SDD)
1. 범용 SSD 볼륨으로 다양한 워크로드에 대해 가격과 성능의 절충안
2. 부팅 볼륨 사용 가능(루트 OS가 실행될 위치에 해당)
- io1/io2(SDD)
1. 최고 성능을 자랑하는 SSD 볼륨으로 미션 크리티컬이자 지연 시간이 낮고 대용량 워크로드에 사용
2. 부팅 볼륨 사용 가능(루트 OS가 실행될 위치에 해당)
- st1(HDD)
1. 저비용의 HDD 볼륨으로 잦은 접근과 처리량이 많은 워크로드에 사용
- sc1(HDD)
1. 가장 비용이 적게 드는 HDD 볼륨으로 접근 빈도가 낮은 워크로드를 위해 설계됨
- EBS 볼륨은 크기, 처리량, IOPS(초당 I/O 작업 수)로 정의

[gp2 VS gp3]
- 범용 gp2와 IOPS 프로비저닝이 가장 중요한 내용으로 시험에 출제됨
- gp2
1. 짧은 지연 시간, 효율적인 비용의 스토리지
2. 시스템 부팅 볼륨에서 가상 데스크톱, 개발, 테스트 환경에서 사용 가능
3. 크기는 1GB ~ 16TB까지 다양함
4. 최대 3,000 IOPS의 1 볼륨과 IOPS가 독립적인 관계가 아닌 링크되어 있어 용량의 GB 수를 3배로 늘릴 때 IOPS 세 배 더 증가하며 최대 16,000 IOPS까지 늘릴 수 있음
- gp3
1. 최신 세대의 볼륨
2. 기본 성능 3,000IOPS와 초당 125MB의 처리량 제공
3. 16,000IOPS와 초당 1,000MB까지 독립적으로 증가 가능

[프로비저닝 IOPS(PIOPS) SSD]
- IOPS 성능을 유지할 필요가 있는 주요 비즈니스 애플리케이션이나 16,000 IOPS 이상을 요하는 애플리케이션에 적합
- 스토리지로 이용하는 경우 데이터베이스 워크로드에 적합
- 이 경우는 스토리지 성능과 일관성에 아주 민감한데 gp2/gp3에서 io1/io2 볼륨으로 바꾸는 것이 해답이 될 수 있음
- io1/io2 중 최신 세대를 선택하는 것이 좋음

[io1 VS io2]
- 4GB ~ 16TB
- Nitro EC2 인스턴스에서는 최대 64,000 IOPS까지 지원
- Nitro EC2 인스턴스가 아닌 경우 최대 32,000 IOPS까지 지원
- io1/io2를 이용하면 gp3 볼륨처럼 프로비저닝된 IOPS를 스토리지 크기와 독자적으로 증가 가능
- io2 장점
1. io1와 동일한 비용으로 내구성과 기가 당 IOPS 수가 더 높음
- io2 Block Express
1. 4GB ~ 64TB
2. 좀 더 고성능 유형의 볼륨
3. 지연 시간이 ms 미만
4. IOPS 대 GB 비율이 1,000:1 일때 최대 256,000 IOPS

[st1 vs sc1]
- 최대 16TB까지 확장가능
- st1
1. 처리량 최적화 HDD
2. 빅 데이터나 데이터 웨어하우징 로그 처리에 적합
3. 최대 처리량은 초당 500MB 그리고 최대 IOPS는 500
- sc1(Cold HDD)
1. 아카이브 데이터용으로 접근 빈도가 낮은 데이터에 적합
2. 최저 비용으로 데이터를 저장할 때 사용
3. 최대 처리량은 초당 250MB 그리고 최대 IOPS도 250

[시험 출제 요건]
- 대략적인 모든 볼륨의 차이
- 범용 SSD VS 프로비저닝 IOPS SSD의 차이
- 데이터 베이스가 필요할 떄와 대용량, 저비용을 요할 때
- st1을 사용하는 경우 그 차이
- 32,000 IOPS 이상을 요할 때는 io1 또는 io2 볼륨의 EC2 Nitro

[EBS Multi Attach]
- 하나의 EBS 볼륨을 같은 AZ에 있는 여러 EC2 인스턴스에 연결할 수 있게 하는 기능
- io1/io2 제품군만 사용 가능
- 각 인스턴스는 고성능 볼륨에 대한 읽기 및 쓰기 권한을 전부 가짐(동시에 읽고 쓰기 가능)
- 해당 AZ 내에서만 사용 가능(한 AZ에서 다른 AZ로 EBS 볼륨 연결 불가능)
- 한 번에 16개의 EC2 인스턴스만 같은 볼륨에 연결 가능(중요!!!)
- 반드시 클러스터 인식 파일 시스템을 사용해야 EBS Multi Attach 이용 가능(XFS, EX4와 같은 파일시스템과 다름)

[EBS Multi Attach 예시]
- Teradata처럼 클러스터링 된 Linux 애플리케이션에서 사용
- 애플리케이션이 동시 쓰기 작업을 관리할 때 사용

[EBS 암호화]
- EBS 볼륨 생성 즉시 암호화 발생
1. 저장 데이터가 볼륨 내부에 암호화
2. 인스턴스와 볼륨 간의 전송 데이터 암호화
3. 스냅샷 뿐만 아니라 스냅샷으로 생성된 볼륨 역시 모두 암호화
- 이러한 암호화는 동시다발적으로 일어남
- 이때 암호화 및 복호화 메커니즘은 보이지 않게 자동으로 처리됨
- 지연 시간에는 거의 영향 없음
- KMS에서 암호화 키를 생성해 AES-256 암호화 표준을 가짐
- 스냅샷을 복사해 암호화를 푼 걸 다시 암호화 활성화를 함

[EBS 암호화 과정]
- 볼륨의 EBS 스냅샷 생성
- 복사 기능을 통해 EBS 스냅샷을 암호화
- 스냅샷을 이용해 새 EBS 볼륨을 생성하면 해당 볼륨도 암호화
- 그 후 암호화된 볼륨을 인스턴스 원본에 연결

[EFS(Elastic File System)]
- EFS는 관리형 NFS(네트워크 파일 시스템)
- NFS이므로 많은 EC2 인스턴스에 마운트 가능
- 서로 다른 AZ영역의 EC2 인스턴스에서도 EFS 기능 가능
- 가용성의 높고 확장성이 뛰어나며 비쌈(GP2 EBS 볼륨의 약 3배)
- 사용량에 따라 비용을 지불하므로 미리 용량을 프로비저닝할 필요 없음

- EFS의 사용 사례는 콘텐츠 관리, 웹 serving, 데이터 공유, Wordpress
- 내부적으로 NFSv4.1 프로토콜을 사용
- EFS에 대한 엑세스를 제어하려면 보안그룹을 설정해야함
- 윈도우가 아닌 Linux 기반 AMI와만 호환됨
- KMS를 사용해서 EFS 드라이브에서 미사용 암호화를 활성화 가능
- Linux 표준 파일 시스템으로 Posix 시스템을 사용하며 표준 파일 API가 있음
- 용량을 미리 설정할 필요 없이 자동으로 확정되며 EFS에서 사용하는 데이터 GB 사용량에 따라 비용을 지불

[EFS의 성능]
- EFS 스케일
1. 동시 NFS 클라이언트 수천 개와 10GB 이상의 처리량을 확보 가능
2. PB 규모의 NFS으로 자동 확장 가능

- NFS 생성 시 성능 모드 설정
1. 범용 : default 값이며 지연 시간에 민감한 사용 사례(웹서버나 CMS)에 사용
2. Max I/O : 지연 시간이 더 긴 NFS이지만 처리량이 높고 병렬성이 높으므로 빅 데이터 애플리케이션이나 미디어 처리가 필요한 경우 유용

- Throughput Mode(처리량 모드)
1. Bursting : 1TB = 초당 50MB ~ 100MB
2. 프로비저닝 : 스토리지 크기에 관계없이 처리량을 설정(ex. 1TB 스토리지 1GiB를 처리)
3. Elastic : 워크로드에 따라 처리량을 자동으로 조절(ex. 읽기는 초당 최대 3GiB, 쓰기는 초당 1GiB까지 가능), 워크로드를 예측하기 어려울 때 유용

[EFS의 스토리지 클래스]
- Storage Tiers
1. 며칠 후 파일을 다른 계층으로 옮길 수 있는 기능
2. EFS Standard 계층은 자주 엑세스하는 파일을 위한 계층이고 자주 엑세스하지 않는 계층은 EFS IA인데, 이 계층에서 파일을 검색할 경우 비용이 발생
3. 하지만 파일을 EFS-IA에 저장하면 비용이 감소
4. EFS_IA를 사용하려면 수명 주기 정책을 사용해해야 함(만약 특정 파일 60일동안 사용하지 않았다면 자동으로 표준 계층에서 EFS_IA 계층으로 이동)

- 가용성 & 내구성
1. 다중 AZ로 EFS를 설정(AZ 하나가 다운되어도 EFS에 영향 미치지 않음)
2. 개발용으로 One Zone EFS을 사용 가능
3. 개발에는 좋지만 하나의 AZ에만 있고 백업은 기본적으로 활성화되도록 설정되어 있으며 엑세스 빈도가 낮은 스토리지 계층과 호환되지 않음
4. 따라서 EFS One Zone IA라고 불리며, 이를 사용하면 굉장히 할인이 많이 됨

- 시험에는 언제 EFS를 사용해야 하는지, NFS에 어떤 옵션을 설정해야 하는지 나옴

[High Availability VS Scalablility]
[확장성(Scalablility)]
- 애플리케이션 시스템이 조정을 통해 더 많은 양을 처리할 수 있다는 의미

- 수직 확장성
1. 인스턴스의 크기를 확장
2. 예시 : t2.micro에서 t2.large로 확장
3. 데이터베이스와 같이 분산되지 않은 시스템에서 흔히 사용
4. RDS나 ElastiCache 등의 데이터베이스에서 쉽게 찾아볼 수 있음
5. 이 서비스들은 하위 인스턴스의 유형을 업그레이드해 수직적으로 확장할 수 있는 시스템들
6. 하드웨어 제한으로 인해 확장할 수 있는 한계가 있음
7. 확장(스케일 업), 축소(스케일 다운)
8. 수직 확장을 통해 매우 작은 인스턴스부터 대규모로 확장 가능

- 수평 확장성
1. 애플리케이션에서 인스턴스나 시스템의 수를 늘리는 방법
2. 수평 확장을 했다는 건 분배 시스템이 있다는 것을 의미
3. 증가(스케일 아웃), 감소(스케인 인)
4. 다른 스케일링 그룹이나 로드 밸런서에도 사용

[고가용성(High Availability)]
- 애플리케이션 or 시스템을 적어도 둘 이상의 AWS의 AZ나 데이터 센터에서 가동 중이라는걸 의미함
- 고가용성의 목표는 데이터 센터에서의 고장에서 생존하는 것으로 센터 하나가 멈춰도 계속 작동하게끔 하는 것
- 고가용성도 RDS 다중 AZ를 갖추고 있다면 수동적일 수 있음(수동형 고가용성)
- 수평 확장하는 경우에는 활성형이 될수도 있음
- 동일 애플리케이션의 동일 인스턴스를 다수의 AZ에 걸쳐 실행하는 경우를 의미
- 다중 AZ가 활성화된 자동 스케일러 그룹이나 로드 밸런서에서도 사용  

[Load Balancing]
- 로드 밸런서는 서버 or 서버set으로 트래픽을 백엔드나 다운스트림 EC2 인스턴스 or 서버들로 전달하는 역할
- 부하를 다수의 다운스트림 인스턴스로 분산하기 위함
- 애플리케이션에 단일 엑세스 지점(DNS)을 노출
- 다운스트림 인스턴스의 장애를 원활히 처리 가능
- 로드 밸런서가 상태 확인 메커니즘으로 어떤 인스턴스로 트래픽을 보낼 수 없는지 확인해줌
- SSL 종료도 할 수 있어서 웹 사이트에 암호화된 HTTPS 트래픽을 가질 수 있음
- 쿠키로 고착도(stickiness) 강화
- 고 가용성 AZ
- 클라우드 내에서 개인 트래픽과 공공 트래픽을 분리할 수 있음

[Elastic Load Balancing(ELB)]
- 관리형 로드 밸런서
- AWS가 관리하며 어떤 경우에도 작동할 것을 보장
- AWS가 업그레이드와 유지 관리 및 고가용성을 책임짐
- 로드 밸런서의 작동 방식을 수정할 수 있게끔 일부 구성 Knob 제공
- 무조건 쓰는 편이 좋음
- 자체 로드 밸런서를 마련하는 것보다 저렴
- 자체 로드 밸런서를 직접 관리하려면 확장성 측면에서 굉장히 번거롭기 때문
- 다수의 AWS의 서비스들과 통합되어 있음
- EC2 인스턴스와도 통합이 가능하며 스케일링 그룹, Amazon ECS와 인증서 관리(ACM), ClouldWatch, Route 53, WAF Global Accelerator 등 앞으로 더 늘어날 예정

[Health Check by ELB]
- Health Check는 ELB가 EC2 인스턴스의 작동이 올바르게 되고 있는지의 여부를 확인하기 위해 사용
- 제대로 작동하는 중이 아니라면 해당 인스턴스로는 트래픽을 보낼 수 없음
- 상태 확인은 포트와 라우트에서 이루어짐

[Types of load balancer on AWS]
- 클래식 로드 밸런서(V1 - 2009 - CLB)
1. HTTP, HTTPS, TCP, SSL (secure TCP)를 지원
2. AWS에서 이 로드밸런서 사용을 권장하지 않음

- Application 로드 밸런서(V2 - 2016- ALB)
1. HTTP, HTTPS, WebSocket 프로토콜 지원

- Network 로드 밸런서(V2 - 2017 - NLB)
1. TCP, TLS (secure TCP), UDP 프로토콜을 지원

- Gateway Load Balancer(2020 - GWLB)
1. 네트워크 층에서 작동하므로 3계층과 IP 프로토콜에서 작동

- 더 많은 기능을 가진 신형 로드 밸런서를 사용하는 것이 권장
- 일부 로드 밸런서들은 내부에 설정될 수 있어 네트워크에 개인적 접근이 가능
- 웹사이트와 공공 애플리케이션 모두에 사용이 가능한 외부 공공 로드 밸런서도 있음

[Load Balancer 보안 그룹]
- 유저는 HTTP나 HTTPS를 사용해 어디서든 로드 밸런서에 접근이 가능
- 포트 범위는 80 or 443
- 소스가 0.0.0.0/0이면 어디든 가능하다는 뜻
- EC2 인스턴스는 로드 밸런서를 통해 곧장 들어오는 트래픽만을 허용해야 하므로 EC2  인스턴스 보안 그룹 규칙은 달라야 함
- 포트 80에서 HTTP 트래픽을 허용하며
- 소스는 IP범위가 아니라 보안그룹이 됨
- EC2 인스턴스의 보안 그룹을 로드 밸런서의 보안 그룹으로 연결
- EC2 인스턴스는 로드 밸런서에서 온 트래픽 만을 허용하게 되는 강화된 보안 메커니즘이 됨

[Application Load Balancer(ALB)]
- 7계층, 즉 HTTP 전용 로드 밸런서
- 머신 간 다수 HTTP 애플리케이션의 라우팅에 사용
- 이러한 머신들은 target group이라는 그룹으로 묶이게 됨
- 동일 EC2 인스턴스 상의 여러 애플리케이션에 부하를 분산(ex. 컨테이너, ECS)
- HTTP/2, WebSocket 및 리다이렉트 지원
- HTTP에서 HTTPS로 트래픽을 자동 리다이렉트하려는 경우 로드밸런서 레벨에서 가능
- 경로 라우팅도 지원
1. target group에 따른 라우팅으로는 예를 들면, URL target route에 기반한 라우팅 가능(example.com/users or example.com/posts)
2. /users와 posts는 URL 상의 서로 다른 경로이고 이들은 다른 target group에 리다이렉트 가능
3. URL의 호스트 이름에 기반한 라우팅로 가능
4. 로드 밸런서가 one.example.com 또는 other.example.com에 접근이 가능하다고 하면 두 개의 다른 대상 그룹에 라우팅 가능
5. 쿼리 문자열과 헤더에 기반한 라우팅 가능(example.com/users?id=123&order=false가 다른 target group에 라우팅 가능)
- ALB는 마이크로 서비스나 컨테이너 기반 애플리케이션에 가장 좋은 로드 밸런서로 도커와 Amazon ECS의 경우 ALB가 가장 적합한 로드 밸런서가 됨
- 왜나하면 포트 매핑 기능이 있어 ECS 인스턴스의 동적 포트로의 리다이렉션을 가능하게 해줌
- CLB 뒤에서 다수의 애플리케이션을 사용하는 경우 실제 애플리케이션 개수만큼의 CLB가 필요
- ALB는 하나만으로 다수의 애플리케이션을 처리할 수 있음

[ALB Target Group]
- EC2 인스턴스
1. HTTP
2. 오토 스케일링 그룹에 의해 관리될 수 있음
- ECS 작업
1. HTTP
- 람다 함수
1. HTTP 요청이 JSON으로 변환됨
2. 람다함수는 AWS에서 무서버로 불리는 모든 것들의 기반이 되는 함수
3. 람다 함수 앞에도 ALB가 있을 수 있음
- IP Address
1. 꼭 private IP여야 함
- ALB는 여러 target group으로 라우팅할 수 있으므로 health check는 target group level에서 이루어짐

[ALB Good to know]
- CLB와 마찬가지로 ALB를 사용하는 경우에도 고정 호스트 이름이 부여
- 애플리케이션 서버는 클라이언트의 IP를 직접 보지 못하며 클라이언트의 실제 IP는 X-Forwarded-For라고 불리는 헤더에 삽입
- X-Forwarded-Port를 사용하는 포트와 X-Forwarded-Proto에 의해 사용되는 프로토콜도 얻게 됨
- 즉, 클라이언트의 IP인 12.34.56.78이 로드 밸런서와 직접 통신하여 연결 종료 기능을 수행
- 로드 밸런서가 EC2 인스턴스와 통신할 때 사설 IP인 로드 밸런서 IP를 사용해 EC2 인스턴스로 들어감
- 그리고 EC2 인스턴스가 클라이언트 IP를 알기 위해서는 HTTP 요청에 있는 추가 헤더인 X-Forwarded-Port와 X-Forwarded-Proto를 확인해야 함

[Network Load Balancer(NLB)]
- L4 로드 밸런서이므로 TCP와 UDP 트래픽을 다룸(HTTP를 다루는 L7보다 하위 계층)
- 성능이 매우 높음(초당 수백만 건의 요청을 처리할 수 있고 지연시간이 400ms인 ALB에 비해 100ms로 지연시간도 짧음)
- AZ별로 하나의 고정 IP를 가짐
- 탄력적 IP 주소를 각 AZ에 할당 가능
- 여러 개의 고정 IP를 가진 애플리케이션을 노출할 때 유용
- 탄련적 IP를 사용할 수 있으므로 1~3개의 IP로만 엑세스할 수 있는 애플리케이션에 고려 가능
- AWS 프리티어에 포함되지 않음
- 백엔드, 프론트엔드 모두 TCP 트래픽을 사용하거나 백엔드에서는 HTTP를 프론트엔드에서는 TCP를 사용할 수 있음

[NLB - Target Group]
- EC2 인스턴스
1. NLB가 TCP 또는 UDP 트래픽을 EC2 인스턴스로 리다이렉트 할 수 있음
- IP Address
1. IP 주소는 반드시 하드코딩되어야 하고 private IP여야 함
2. 자체 EC2 인스턴스의 private IP를 보낼 수 도 있지만 자체 데이터 센터 서버의 private IP를 사용할 수 있기 때문
3. 둘 다 같은 NLB를 앞에 사용 가능하기 때문
- ALB
1. NLB를 ALB 앞에 배치하는 경우
2. NLB 덕분이 고정 IP 주소를 얻을 수 있고 ALB 덕분에 HTTP 유형의 트래픽을 처리하는 규칙을 얻을 수 있기 때문
- NLB Target Group이 수행하는 Health Check
1. TCP, HTTP, HTTPS 프로토콜 지원
2. 백엔드 애플리케이션이 HTTP, HTTPS 프로토콜을 지원한다면 해당 프로토콜에 대한 상태확인을 정의할 수 있음
