# AWS SAA

### Getting started with AWS
1. AWS Regions
- 데이터 센터의 집합
2. AWS 리전 선택 방법
- 법률 준수 
- 지연 시간 : 대부분의 사용자가 미국에 있다면 미국 리전을 선택하는 것이 지연시간 감소
- 사용하고자 하는 서비스가 있는 리전 선택
- 요금 : 리전별로 요금 상이
3. 가용영역 (aws avaliability zones)
- 한 리전에 여러 가용영역 존재
- 가용영역은 하나 또는 두 개의 개별적인 데이터센터로 구성
- 데이터센터 < 가용영역 < 리전
4. 엣지 로케이션
- 40여 국가의 90개 이상의 도시에 400개가 넘는 전송 지점 존재
- 엣지 로케이션을 통해 최소 지연 시간으로 컨텐츠 전달 가능


### IAM
1. IAM User & Groups
- root 계정은 계정을 생성할 때만 사용
- 그 이후는 사용자를 생성해서 사용
- 여러 사용자를 하나의 그룹으로 관리
- 그룹 내에는 사용자만 설정 가능 (그룹안에 그룹 관리 불가)
- 한 사용자가 여러 그룹에 속하는 것은 가능
2. IAM Permissions
- 생성한 사용자에게 권한 부여 가능
3. IAM Policies inheritance
- IAM 그룹 별로 정책 적용 가능
- 그룹에 속하지 않은 사용자는 인라인정책으로 적용 가능
- 한 명이 여러 그룹에 속한 경우 각 그룹의 정책이 모두 적용됨
- 커스텀하여 신규 정책 생성 가능
4. IAM Policies Structure
```JSON
{
	"Version":"2012-10-17",
	"Id":"S3-Account-Permissions",
	"Statement":[
		{
			"Sid":"1",
			"Effect":"Allow",
			"Principal": {
				"AWS":["arn:aws:iam::123456789012:root"]
			},
			"Action":[
				"s3:GetObject",
				"s3:PutObject"
			],
			"Resource": ["arn:aws:s3:::mybucket/*"]
		}
	]
}
```

- Version: 정책 언어 버전
- Id: 정책 식별자(선택 사항)
- Statement: 하나 이상의 개별 명세서(필수)
- Sid: 명령문의 식별자(선택 사항)
- Effect: 액세스를 허용하거나 거부하는지 여부(Allow, Deny)
- Principal: 이 정책이 적용된 계정/사용자/역할
- Action: 이 정책이 허용하거나 거부하는 작업 목록
- Resource: 작업이 적용되는 리소스 목록
5. IAM Password Policy - MFA (Multi Factor Authentication)
- 비밀번호와 보안장치를 함께 사용하는 방식
- 자신의 비밀번호와 MFA 생성 토큰 사용
6. MFA Devices options in AWS
- 가상 MFA 장치 (google authenticator, authy ...)
- U2F 보안키
- 하드웨어 키 팝 MFA 장치
7. IAM Roles for Services
- AWS 서비스에 권한을 부여하기 위해 사용 (AWS 서비스 별 권한 적용)
- 예를 들어 AWS EC2 인스턴스에서 AWS의 어떤 정보에 접근할 때 사용하는 권한
8. IAM Security Tools (보안도구)
- IAM 자격 증명 보고서
- IAM 액세스 관리

### AWS 접근 방법
1. AWS Management console
2. AWS 명령줄 인터페이스 (CLI)
- 리소스를 관리하는 스크립트를 통해 작업 자동화 가능
- 액세스키를 통해 접근 (액세스키, 비밀액세스키)
3. AWS 소프트웨어 개발 키트 (SDK)
- 코딩을 통해 애플리케이션 내에 심어 두어서 사용
- 다양한 프로그래밍 언어 지원(JavaScript Python, PHP, .NET, Ruby, Java, Go Node.js, C++)
4. AWS CloudShell
- CLI 대체하여 사용
- 저장소 사용 가능

### IAM 모범 사례 및 요약
1. 모범 사례
- AWS 계정 설정 외에는 루트 계정을 사용 금지
- 물리적 사용자 1명 = AWS 사용자 1명
- 사용자를 그룹에 할당하고 그룹에 권한을 할당
- 강력한 비밀번호 정책 생성
- 다단계 인증(MFA) 사용 및 시행
- AWS 서비스에 권한을 부여하기 위한 역할 생성 및 사용
- 프로그래밍 방식 액세스를 위한 액세스 키 사용(CLI/SDK)
- IAM 자격 증명 보고서 및 IAM 액세스 어드바이저을 사용하여 계정 권한을 감사
- IAM 사용자 및 액세스 키 공유 금지
2. 요약
- 사용자: 물리적 사용자에 매핑되며 AWS 콘솔에 대한 비밀번호가 존재
- 그룹: 사용자만 포함
- 정책: 사용자 또는 그룹의 권한을 설명하는 JSON 문서
- 역할: EC2 인스턴스 또는 AWS 서비스용
- 보안: MFA + 비밀번호 정책
- AWS CLI: 명령줄을 사용하여 AWS 서비스를 관리
- AWS SDK: 프로그래밍 언어를 사용하여 AWS 서비스를 관리
- 액세스 키: CLI 또는 SDK를 사용하여 AWS에 액세스
- 감사: IAM 자격 증명 보고서 및 IAM 액세스 관리자
