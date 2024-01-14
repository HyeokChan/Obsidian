
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
- 
