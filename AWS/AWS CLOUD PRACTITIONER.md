
# AWS CLOUD PRACTITIONER

# 목차
1. 액세스 하는 3가지 방법
- AWS management console
- 명령줄 인터페이스
- 소프트웨어 개발키드
2. 컴퓨팅
- amazon ec2 (elastic computing cloud)
- ec2 container service
- ec2 container registry
- amazon lightsail
- aws batch
- aws elastic beanstalk
- aws lambda
- auto sacaling
3. 스토리지
- amazon s3 (simple storage service)
- amazon elastic block store
- amazon elastic file system
- amazon glacier
- aws sotrage gateway
4. 데이터베이스
- amazon aurora
- amazon rds (relational database service)
- amazon dynamo db
- amazon elasticache
5. 마이그레이션
- aws application discovery service
- aws database migration service
- aws server migration service
- aws snowball
- aws snowball edge
- aws snowmobile
6. 네트워킹과 컨텐츠 전송
- amazon vpc (virtual private cloud)
- amazon cloudfront
- amazon route 53
- aws direct connect
- elastic load balancing (elb)
7. 개발자도구
- aws code commit
- aws code build
- aws code deploy
- aws code pipeline
- aws x-ray
8. 관리도구
- amazon cloudwatch
- amazon ec2 systems manager
- amazon cloudformation
- aws cloudtrail
- aws config
- aws opsworks
- aws service catalog (marketplace)
- aws trusted advisor
- aws personal health dashboard
- aws managed services
9. 보안, 자격증명 및 보안준수
- amazon cloud directory
- aws iam (identity and access management)
- amazon inspector
- amazon certificate manager
- aws cloudHSM
- aws directory service
- aws key management service
- aws organizations
- aws shield
- aws WAF
10. 분석
- amazon athena
- amazon EMR
- amazon elasticsearch service
- amazon kinesis
- amazon redshift
- amazon quicksight
- amazon data pipeline
- amazon glue
11. 인공지능
- amazon lex
- amazon polly
- amaone rekoginition
- amazon machine learning
12. 모바일 서비스
- aws mobild hub
- amazon cognito
- amazon pinpoint
- amazon device farm
- aws mobile sdk
- amazon mobile analytics
13. 애플리케이션 서비스
- aws step functions
- amazon api gateway
- amazon elastic transcoder
- amazon SWF (simple work flow)
14. 메시징
- amazon SQS (simple queue service)
- amazon SNS (simple notification service)
- amazon SES (simple mail service)
15. 기업생산성
- amazon workdocs
- amazon workmail
- amazon chime
16. 데스크톱 및 앱 스트리밍
- amazon workspaces
- amazon appstream 2.0
17. 사물 인터넷
- aws iot 플랫폼
- aws greengrass
- aws iot 버튼
18. 게임 개발
- amazon gamelift
- amazon lumberyard

# 주요 개념 정리
- aws 보안, 공동 책임 모델 : aws는 클라우드 자체의 보안을 관리하지만 클라우드 내에서 보안을 유지하는 것은 고객의 책임

### 액세스 하는 3가지 방법 (amazon web service에 액세스)
1. aws management console
- 모바일 앱도 사용 가능
2. aws 명령줄 인터페이스 (cli)
3. 소프트웨어 개발 키트 (sdk) 
- 프로그래밍 언어 및 플랫폼에 맞게 사용 가능

### 컴퓨팅
1. amazon ec2
- amazon ec2 인스턴스
- 대부분의 aws 서비스와 통함
- 신속하게 용량 확장 및 축소
- 인스턴스가 vpc 내에 위치. 인터넷에 공개할 인스턴스, 공개하지 않을 인스턴스 지정 가능
- 보안그룹 및 acl(액세스 제어 목록)을 통해 인바운드, 아웃바운드 네트워크 액세스 제어 가능
- 온디맨드 인스턴스 : 완전 종량제, 언제든지 종료 가능
- 예약 인스턴스 : 온디맨드 인스턴스에 비해 대폭 할인된 금액, 사용기간을 미리 설정함
- 스팟 인스턴스 : 인스턴스를 입찰하여 사용. 스팟 시장에 따라 영향을 받음
2. amazon ec2 container service (ecs)
- docker 컨테이너를 지원하는 컨테이너 관리 서비스
- 사용하면 클러스터 관리를 할 필요가 없음
- ecs : container - docker - 클러스터 관리
3. amazon ec2 container registry (ecr)
- 도커 컨테이너 이미지를 저장, 관리, 배포 도와줌
- ecs와 통합되어 개발에서 프로덕션까지의 워크플로를 간소화
- 자체적인 컨테이너 레포지토리를 사용하지 않아도 됨
4. amazon lightsail
- aws에서 가상 프라이빗 서버를 시작하고 관리할 때 사용할 수 있는 가장 간편한 방식
- 가상머신, ssd, 스토리지, 데이터전송, dns 관리, 고정 ip주소도 포함되어 있음
- 가벼운 방식, 가상 프라이빗 서버
5. aws batch
- aws에서 배치 컴퓨팅 작업을 효율적으로 수행
- 결과분석, 문제해결에 집중 가능
- batch -> batch 컴퓨팅 작업
6. aws elastic beanstalk
- java, .net, php, node.js, python, ruby, go, docker를 이용하여 apache, nginx, passenger, lis 같은 친숙한 서버에서 개발된 웹 애플리케이션 서비스를 배포하고 확장하는 서비스
- 코드 개발에 집중할 수 있음 (코드만 올리면 됨)
7. aws lambda
- 서버를 프로비저닝(관리) 할 필요 없이 코드를 실행할 수 있음
- lambda : 간편, 바로 실행 -> 서버없이 코드로 실행
8. auto scaling
- amazon ec2의 인스턴스 개수를 자동으로 확대/축소
- ec2 자체는 지정해둔 인스턴스의 용량만 가변적으로 사용
- auto scaling : ec2 인스턴스 개수 증가/감소

### 스토리지
1. amazon S3
- 웹 어느곳에서든지 용량에 관계없이 데이터를 저장하고 검색할 수 있는 단순한 웹 서비스 인터페이스를 갖춘 객체 스토리지
2. amazon elastic block store (EBS)
- ec2에 사용할 영구 블록 스토리지 볼륨 제공
- 데이터를 블록 단위로 저장하고 관리하는 스토리지 형태
- 고성능 볼륨, 가용성, 암호화, 액세스관리, 스냅샷(EBS->S3)
4. amazon elastic file system (EFS)
- ec2에 사용할 간단하고 확장가능한 파일 스토리지 제공
5. amazon glacier
- 데이터보관 및 장기백업을 위한 스토리지
- 비용을 낮게 유지하면서 동시에 다양한 검색 요구를 지원하기 위해 아카이브에 액세스하는 3가지 옵션 제공
- glacier : 빙하 -> 장기백업, 데이터보관
6. aws storage gateway
- 온프레미스 스토리지 환경과 aws 클라우드 양쪽을 넘나들며 하이브리드 스토리지 사용 가능

### 데이터베이스
1. amazon aurora
- amazon의 자체 개발된 클라우드 네이티브 데이터베이스 엔진
- mysql 및 postgreSQL과 호환되는 데이터베이스 엔진
- 고성능, 뛰어난 보안(VPC, KMS), mysql, postgreSQL 호환성, 높은 확장성, 높은 가용성 및 내구성, 완전 관리형
2. amazon RDS
- mysql, postgreSQL, oracle, mariaDB 등 다양한 데이터베이스 엔진 지원 (선택해서 사용)
3. amazon dynamoDB
- 어떤 상황에서든 지연시간이 일관적으로 한 자릿수 밀리초 단위여야 하는 애플리케이션을 위한 빠르고 유연한 NoSQL 데이터베이스 서비스
- 모바일, 웹, 게임, 광고 기술, iot에 적합
- 자동분할, ssd 기술 사용
- 이벤트 중심 프로그래밍 : aws lambda에 통합되어 데이터 변경 시마다 자동으로 반응하는 트리거 제공
- 세분화된 액세스 제어 : aws IAM과 통합되어 액세스 제어
- dynamoDB : 지연시간 일관, NoSQL, 이벤트 중심, Lambda
4. amazon ElastiCache
- 클라우드에서 인메모리 캐시를 손쉽게 배포, 운영, 조정 제공 서비스
- 인메모리 캐시 : Redis, memcached 지원

### 마이그레이션
1. aws application discovery service
- 마이그레이션을 위한 정보 수집에 이용
- 온프레미스 데이터 센터에서 실행되는 애플리케이션, 종속성, 성능 프로파일 식별
- application discovery service : 마이그레이션을 위한 정보 식별, 수집
2. aws database migration service (DMS)
- database를 aws로 마이그레이션
- 이기종 데이터베이스 마이그레이션 (MySQL->PostgreSQL) 지원함
3. aws server migration service (SMS)
- 수 천개의 온프레미스 워크로드를 aws로 쉽고 빠르게 마이그레이션 할 수 있음
4. aws snowball
- 페타바이트 규모 데이터 전송 솔루션
- 전송이 완료되고 어플라이언스를 반환할 준비가 되면 전자 잉크 배송 라벨이 자동으로 업데이트 되고 amazon simple notification service (SNS) 또는 텍스트 메시지를 사용하거나 콘솔에서 직접 작업 상태를 추적할 수 있음
5. aws snowball edge
- aws snowball 과 유사하지만 추가 기능 있음 (데이터처리, 데이터분석)
6. aws snowmobile
- 엑사바이트 규모의 대규모 데이터 전송 솔루션

### 네트워킹과 컨텐츠 전송
1. amazon virtual private cloud (VPC)
- 고객이 정의한 가상 네트워크에서 aws 리소스를 시작할 수 있도록 aws 클라우드에서 논리적으로 격리된 공간을 프로비저닝 할 수 있음
- 가상 네트워킹 환경을 완벽히 제어할 수 있음(ip주소, 서브넷, 라우팅)
- vpc에서 ipv4, ipv6을 모두 사용하여 애플리케이션과 리소스에 액세스할 수 있음
- 페지싱 서브넷에 백엔드시스템 배치
- 보안 그룹 및 네트워크 액세스 제어 목록을 포함한 다중 보안 계층을 활용하여 각 서브넷에서 ec2 인스턴스에 대한 액세스를 제어하도록 지원 가능
- 기업 데이터 센터와 vpc 사이에 vpn 연결을 생성하여 aws 클라우드를 기업 데이터센터의 확장으로 활용 가능
- vpc : 가상 네트워크, 페이싱 서브넷, ec2 인스턴스 액세스 제어, vpn 연결 기업 데이터센터
2. amazon cloudFront
- 웹 사이트, api, 동영상 콘텐츠 또는 기타 웹 자산의 전송 가속화
- 콘텐츠 전송 능력이 뛰어남
- cloudFront : Front -> 콘텐츠 -> 네트워크 콘텐츠 전송
3. amaon route 53
- 클라우드 DNS 웹 서비스
- 도메인 -> IP 변환, ipv6 지원
- 사용자를 aws 외부의 인프라로 라우팅 하는 데에도 사용할 수 있음
4. aws direct connect
- 온프레미스 - aws 전용 네트워크 설정
- direct connect : 온프레미스 - aws 네트워크 직접(direct) 연결
5. elastic load balancing (ELB)
- 수신되는 애플리케이션 트래픽을 여러 ec2 인스턴스로 배포
- classic load balancer : 일반 트래픽 라우팅
- application load balancer : 고급 라우팅 기능, 마이크로 서비스

### 개발자 도구
1. aws codecommit
- git repository 호스팅
2. aws codebulid
- 소스 컴파일, 테스트, 빌드 서비스
3. aws codeDeploy
- ec2 인스턴스, 온프레미스 인스턴스 코드 배포 서비스
4. aws codepipeline
- 애플리케이션 및 인프라를 빠르고 안정적으로 업데이트 할 수 있는 지속적 통합 및 전송 서비스
- 코드가 변경될 때마다 코드를 구축, 테스트 배포
5. aws x-ray
- 애플리케이션과 기본서비스가 어떻게 작동하는지 확인
- 분석 도구 : x-ray로 찍어본 것 처럼 프로세스 확인

### 관리 도구
1. amazon cloudwatch
- aws 클라우드 리소스 및 애플리케이션을 모니터링 하는 서비스
- 지표, 로그 수집
- aws 리소스 변경에 자동으로 대응
- 리소스 사용률, 애플리케이션 성능, 운영 상태 파악
2. amazon ec2 system manager
- 소프트웨어 인벤토리 수집, 운영체제 패치 적용, 시스템 이미지 생성
- window 및 linux 운영체제 구성을 자동화 해주는 관리 서비스
3. aws cloud formation
- aws 리소스 모음을 생성 및 관리하고 순서에 따라 예측 가능한 방식으로 프로비저닝 하고 업데이트 할 수 있음
- cloud formation : 폼, 포맷 -> 리소스 폼 -> 리스소 모음 생성/관리
4. aws cloudTrail
- 계정에 대한 aws 호출을 기록하고 로그 파일을 사용자에게 전달하는 웹 서비스
- cloudTrail : 트레일 -> 로그 쭉 쌓임 -> 로그파일을 사용자에게 전달
5. aws config
- aws 리소스 인벤토리, 구성 기록, 구성 변경 알림을 제공하여 보안 및 거버넌스를 실현하는 완전 관리형 서비스
- config rules, 규정 준수 상태
6. aws opsworks
- 구성 관리 서비스
- chef (서버 구성을 코드로 취급하는 자동화 플랫폼)
- ec2, 온프레미스 인스턴스 구성, 배포, 관리하는 작업
7. aws service catalog
- aws에서 사용이 승인된 서비스 카탈로그를 생성하고 관리
- 흔히 배포되는 it서비스를 중앙에서 관리할 수 있음
8. aws trusted advisor
- aws 환경을 최적화하여 비용을 줄여주고 성능을 향상시키며 보안을 개선하는 온라인 리소스
- aws 모범사례에 따라 리소스를 프로비정하는게 도움이 되는 실시간 지침 제공
- trusted advisoir : 믿을만한 조언자 -> aws 환경 최적화, 비용 감소, 보안 개선
9. aws personal health dashboard
- aws가 고객에게 영향을 미칠 수 있는 이벤트를 겪고 있을 때 이를 알리고 수정 지침을 제공
10. aws managed services
- aws에서 인프라를 지속적으로 관리하므로 사용자는 애플리케이션에 집중 가능

### 보안, 자격 증명 및 규정 준수
1. aws cloud directory
- 여러 차원에 걸쳐 데이터 계층을 조직할 수 있는 유연한 클라우드 기반 디렉토리 구축
2. aws identity and access management (IAM)
- 사용자의 aws 서비스와 리소스에 대한 액세스를 통제
- aws 사용자 및 그룹을 만들고 관리하며 권한을 사용하여 aws 리소스에 대한 액세스를 허용 및 거부 가능
- IAM 사용자 관리, IAM 역할 및 권한 관리, 연합된 사용자 관리
3. amazon inspector
- aws 배포된 애플리케이션 자동 보안 평가 서비스
- 애플리케이션의 취약점 또는 모범사례와의 차이 평가
4. aws certicate manager
- aws 서비스에 사용할 ssl/tls 인증서 관리 및 배포 서비스
5. aws cloudHSM
- aws 클라우드 내의 전용 하드웨어 보안 모듈(HSM) 어플라이언스를 사용하여 데이터 보안에 도움을 줌
6. aws directory service
7. aws key management service (KMS)
- 데이터 암호화에 사용되는 암호화 키를 쉽게 생성하고 제어할 수 있게 해주는 관리 서비스
- cloudTrail과 통합되어 모든 키 사용에 대한 로그 제공 가능
8. aws organizations
- aws 계정 그룹을 생성하고 이를 사용해 보안 및 자동화 설정 및 관리
9. aws shield
- aws 웹 애플리케이션 디도스 보호 서비스
- aws shield standard
- aws shield advanced
10. aws WAF
- 애플리케이션 가용성에 영향을 주거나 보안을 약화하거나 리소스를 과도하게 사용하는 일반적인 웹도용으로부터 웹 애플리케이션을 보호하는 방화벽 서비스
- 어떤 트래픽에 웹 애플리케이션에 대한 액세스를 허용하거나 차단할 지 제어 가능
- sql injection, css 공격 패턴 차단

### 분석
1. amazon athena
- 표준 SQL로 amazon S3 데이터를 분석할 수 있는 대화식 쿼리 서비스
- 서버리스 서비스, 실행한 쿼리에 대해서만 비용 지불
2. amazon EMR
- ec2 인스턴스 전반에 걸쳐 대량의 데이터 처리를 지원하는 관리형 하둡 프레임워크 제공
- 로그분석, 웹 인덱싱, 데이터 변환, 기계학습, 금융분석, 과학적 시뮬레이션 등 빅 데이터 사용 사례 처리
3. amazon cloudSearch
- 검색 솔루션 설정, 관리 서비스
4. amazon elasticsearch service
- 로그분석, 전체 텍스트 검색, 애플리케이션 모니터링
5. amazon kinesis
- aws 스트리밍 데이터 플랫폼
- 스트리밍 데이터를 로드 및 분석 기능 제공
- amazon kenesis firehose : 가장 간편
- amazon kinesis analytics : 표준 SQL로 처리
- amazon kinesis streams : 특수 요구에 맞게 커스텀
- kinesis : 대량 -> aws 스트리밍 데이터 분석
6. amazon redshift
- 페타바이트 규모의 완전 관리형 데이터 웨어 하우스
7. amazon quicksight
- 클라우드 기반의 빠른 비즈니스 분석 서비스
- 데이터 시각화 구축, 임시 분석
8. aws data pipeline
- 지정된 간격으로 데이터를 안정적으로 처리하고 이동할 수 있도록 지원하는 웹 서비스
9. aws glue
- 데이터 스토어 사이에 데이터를 쉽게 이동시킬 수 있는 완전 관리형 ETL 서비스
- 데이터 검색, 변환, 매핑 단순화 및 자동화

### 인공지능
1. amazon lex
- 음성과 텍스트를 사용하는 애플리케이션 대화형 인터페이스 서비스
2. amazon polly
- 텍스트를 음석으로 변환하는 서비스 (TTS)
3. amazon machine learning
- 기계학습 서비스

### 모바일 서비스
1. amazon mobile hub
- 통합 콘솔 사용환경을 사용하여 모바일 앱 백엔드 기능을 빠르게 생성, 모바일 백엔드 키트
2. amazon cognito
- 사용자 가입 및 로그인 기능
3. amazon pinpoint
- 지정한 대상에 대한 캠페인 실행, 참여 유도
4. aws device farm
- 앱 테스트 서비스, 한번에 많은 디바이스에서 테스트
5. aws mobile sdk
- 고품질 모바일 앱 개발 지원, 다양한 aws 서비스 액세스
6. amazon mobile anaytics
- 앱 사용량 및 앱 수익 측정

### 애플리케이션 서비스
1. aws step function
- 시각적 워크플로를 사용해 분산 애플리케이션 및 마이크로 서비스의 구성요소와 단계를 손쉽게 조정
- 구성 요소를 일련의 단계로 배열 및 시각화
2. amazon api gateway
- 트래픽 관리, 권한 부여 및 액세스 제어, 모니터링, api 버전 관리
- 프런트 도어 역할을 하는  api 생성 가능
3. amazon elastic transcoder
- 클라우드에서 미디어 트랜스코딩 제공
- 미디어 파일을 스마트폰, 태플릿, pc에서 재생할 버전으로 변환
4. amazon SWF (Simple Work Flow)
- 백 그라운드 작업을 빌드, 실행, 규모 조정

### 메시징
1. amazon SQS (Simple Queue Service)
- 완전 관리형 메시지 대기열 서비스
2. amazon SNS (Simple Notification Service)
- 완전 관리형 푸시 알림 서비스
3. amazon SES (Simple Email Service)
- 이메일 서비스

### 기업 생산성
1. amazon workdocs
- 엔터프라이즈 스토리지 공유 서비스
2. amazon workMail
- 비즈니스 이메일 및 일정 서비스
3. amazon chime
- 온라인 미팅 통신 서비스

### 데스크톱 및 앱 스트리밍
1. amazon workspaces
- 데스크톱 컴퓨팅 서비스
2. amazon appstream 2.0
- 완전 관리형 애플리케이션 스트리밍 서비스
- aws에서 웹 브라우저를 실행하는 모든 디바이스로 스트리밍

### 사물 인터넷
1. aws iot 플랫폼
- 디바이스가 클라우드 애플리케이션을 실행하도록 관리, 처리
2. aws greengrass
- 연결된 장치에 대해 로컬 컴퓨팅, 메시징 및 데이터 캐싱 처리
- 인터넷에 연결되어 있지 않더라도 커넥티드 디바이스에서 aws lambda 실행, 디바이스 데이터 동기화
3. aws iot 버튼
- amazon dash button 하드웨어를 기반으로한 프로그램 가능한 버튼

### 게임 개발
1. amazon game lift
- 멀티플레이어 등 게임서버
2. amazon lumberyard
- 무료 크로스플랫폼 3D 게임 엔진

