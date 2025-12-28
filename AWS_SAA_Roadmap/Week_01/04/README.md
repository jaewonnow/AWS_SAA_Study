# Placeholder
## Q1 (pdf Q#3)
한 회사가 AWS Organizations를 사용하여 여러 부서의 AWS 계정을 관리하고 있습니다. 관리 계정에는 프로젝트 보고서가 저장된 Amazon S3 버킷이 있습니다. 이 회사는 AWS Organizations 내 조직 계정 사용자만 해당 S3 버킷에 접근할 수 있도록 접근 권한을 제한하고자 합니다. 이러한 요구 사항을 충족하면서 운영 오버헤드를 최소화하는 솔루션은 무엇일까요?

AWS Organizations 내 조직 계정 사용자만 해당 S3 버킷에 접근할 수 있도록 접근 권한을 제한, 운영 오버헤드를 최소화하는 솔루션

A. 조직 ID를 참조하는 `aws:PrincipalOrgID` 전역 조건 키를 S3 버킷 정책에 추가합니다.
B. 각 부서별로 조직 단위(OU)를 생성합니다. `aws:PrincipalOrgPaths` 전역 조건 키를 S3 버킷 정책에 추가합니다.
C. AWS CloudTrail을 사용하여 `CreateAccount`, `InviteAccountToOrganization`, `LeaveOrganization`, `RemoveAccountFromOrganization` 이벤트를 모니터링합니다. S3 버킷 정책을 accordingly 업데이트합니다.
D. S3 버킷에 액세스해야 하는 각 사용자에게 태그를 지정합니다. `aws:PrincipalTag` 전역 조건 키를 S3 버킷 정책에 추가합니다.

https://ai-soyoung.tistory.com/entry/AWS-SAA-IAM
https://jibinary.tistory.com/323

**aws:PrincipalOrgID** -> AWS 조직 멤버 계정에만 리소스 정책 적용 제한(가장 단순하고 유지보수 부담이 적음)
**aws:PrincipalOrgPaths** Organization의 특정 OU 조직 유닛(OU)의 계층을 지정하여 특정 부서나 그룹에 대한 세밀한 접근을 제어
(보안 제어는 더 세밀하지만 운영 오버헤드가 큼)
**aws:PrincipalTag** → AWS IAM 정책에서 요청을 수행하는 보안 주체(Principal, 사용자 또는 역할 등)에 연결된 태그를 기반으로 액세스를 제어할 때 사용되는 글로벌 조건 키
(대규모 환경에서 관리 매우 번거로움)

정답 : A

## Q2 (pdf Q#17)
한 회사가 새로운 비즈니스 애플리케이션을 구축하고 있습니다. 이 애플리케이션은 두 개의 Amazon EC2 인스턴스에서 실행되며 문서 저장을 위해 Amazon S3 버킷을 사용합니다. 솔루션 아키텍트는 EC2 인스턴스가 S3 버킷에 접근할 수 있도록 해야 합니다. 이 요구 사항을 충족하기 위해 솔루션 아키텍트는 무엇을 해야 할까요?

솔루션 아키텍트는 EC2 인스턴스가 S3 버킷에 접근할 수 있도록 해야 합니다.

A. S3 버킷에 대한 접근 권한을 부여하는 IAM 역할을 생성하고, 해당 역할을 EC2 인스턴스에 연결합니다.
B. S3 버킷에 대한 접근 권한을 부여하는 IAM 정책을 생성하고, 해당 정책을 EC2 인스턴스에 연결합니다.
C. S3 버킷에 대한 접근 권한을 부여하는 IAM 그룹을 생성하고, 해당 그룹을 EC2 인스턴스에 연결합니다.
D. S3 버킷에 대한 접근 권한을 부여하는 IAM 사용자를 생성하고, 해당 사용자 계정을 EC2 인스턴스에 연결합니다.

https://velog.io/@captain-yun/AWS-%EB%A6%AC%EC%86%8C%EC%8A%A4%EC%97%90-%EC%A0%91%EA%B7%BC%ED%95%98%EB%8A%94-%EB%B0%A9%EC%8B%9D

**IAM 역할(Role)** 자격 증명을 직접 관리할 필요 없이 AWS 서비스나 애플리케이션에 임시 권한을 부여하는 방식입니다. 역할은 AWS 서비스 간 안전한 통신을 위해 많이 사용됩니다. EC2, Lambda, ECS 같은 AWS 서비스에서 다른 서비스(S3, RDS 등)에 접근할 때 주로 사용됩니다.
(우선순위: 1위 - 보안성이 매우 높고, AWS 서비스 간 통신에 필수적)

정답 : A

## Q3 (pdf Q#89)
한 회사가 기밀 감사 문서를 저장하기 위해 Amazon S3를 사용합니다. S3 버킷은 버킷 정책을 사용하여 최소 권한 원칙에 따라 감사팀 IAM 사용자 자격 증명으로만 접근을 제한합니다. 회사 관리자들은 S3 버킷에 저장된 문서가 실수로 삭제될 것을 우려하여 더 안전한 솔루션을 원합니다. 솔루션 아키텍트는 감사 문서를 보호하기 위해 무엇을 해야 할까요?

S3 버킷에 저장된 문서가 실수로 삭제될 것을 우려하여 솔루션 아키텍트는 감사 문서를 보호하기 위해 무엇을 해야 할까요.

A. S3 버킷에서 버전 관리 및 MFA 삭제 기능을 활성화합니다.
B. 각 감사팀 IAM 사용자 계정에 대해 다단계 인증(MFA)을 활성화합니다.
C. 감사 기간 동안 s3:DeleteObject 작업을 거부하도록 감사팀 IAM 사용자 계정에 S3 수명 주기 정책을 추가합니다.
D. AWS 키 관리 서비스(AWS KMS)를 사용하여 S3 버킷을 암호화하고 감사팀 IAM 사용자 계정이 KMS 키에 액세스하지 못하도록 제한합니다.

https://ysh2.tistory.com/193
https://iwantbaobab.tistory.com/633

**S3 MFA Delete** S3 버킷의 객체를 삭제하거나 버전 관리를 변경할 때, MFA (Multi-Factor Authentication)를 요구함으로써 의도치 않은 또는 악의적인 삭제로부터 보호하는 기능이다.

정답 : A

## Q4 (pdf Q#96)
Amazon EC2 관리자가 여러 사용자가 포함된 IAM 그룹과 연결된 다음 정책을 생성했습니다. 이 정책의 효과는 무엇입니까?

A. 사용자는 us-east-1 리전을 제외한 모든 AWS 리전에서 EC2 인스턴스를 종료할 수 있습니다.
B. 사용자는 us-east-1 리전에서 IP 주소가 10.100.100.1인 EC2 인스턴스를 종료할 수 있습니다.
C. 사용자의 소스 IP가 10.100.100.254인 경우, 사용자는 us-east-1 리전에서 EC2 인스턴스를 종료할 수 있습니다.
D. 사용자의 소스 IP가 10.100.100.254인 경우, 사용자는 us-east-1 리전에서 EC2 인스턴스를 종료할 수 없습니다.

https://jibinary.tistory.com/59

**Effect** : "Allow (허용)" or "Deny (거부)"   
**Action** : AWS 리소스에서 어떤 작업을 실행할지 ("Action": "s3:PutObject" : S3 버킷에 객체를 업로드할 수 있는 권한)
**Resource** : Action의 대상(AWS 리소스) ("Resource": "arn:aws:s3:::my-bucket/*" : 특정 S3 버킷의 모든 객체 )
**Principal** : Action을 수행하려는 주체. 이는 특정 IAM User, Role이거나 AWS 서비스가 해당된다.
                "Principal": {"AWS": "arn:aws:iam::account-id:user/user-name"} : 특정 IAM 사용자
                "Principal": {"Service": "lambda.amazonaws.com"} : AWS Lambda 서비스
**Condition** : Policy가 적용되는 조건 (예: 특정 IP 주소 범위에서의 액세스)
                "Condition": {"IpAddress": {"aws:SourceIp": "203.0.113.0/24"}} : 특정 IP 주소 범위에서의 액세스만 허용

statement 2 (Deny) 조건에 의해 us-east-1 제외한 모든 리전은 Deny된다.
Statement 1 (Allow) 조건에 의해 Source IP가 10.100.100.0/24 일 때 -> EC2 종료 허용

정답 : C

## Q5 (pdf Q#109)
한 회사가 Amazon S3에 데이터를 저장해야 하며, 데이터가 변경되지 않도록 보호해야 합니다. 회사는 Amazon S3에 새로 업로드되는 객체가 특정 기간 동안 변경되지 않은 상태로 유지되기를 원하며, 회사가 객체를 수정하기로 결정할 때까지 변경되지 않도록 해야 합니다. 또한, 회사 AWS 계정의 특정 사용자만 해당 객체를 삭제할 수 있는 권한을 가져야 합니다. 솔루션 아키텍트는 이러한 요구 사항을 충족하기 위해 무엇을 해야 할까요?

A. S3 Glacier 볼트를 생성합니다. 객체에 쓰기 전용, 읽기 전용(WORM) 볼트 잠금 정책을 적용합니다.
B. S3 객체 잠금이 활성화된 S3 버킷을 생성합니다. 버전 관리를 활성화합니다. 보존 기간을 100년으로 설정합니다. 새 객체에 대한 S3 버킷의 기본 보존 모드로 거버넌스 모드를 사용합니다.
C. S3 버킷을 생성합니다. AWS CloudTrail을 사용하여 객체를 수정하는 모든 S3 API 이벤트를 추적합니다. 알림이 오면 회사에서 보유한 백업 버전에서 수정된 객체를 복원합니다.
D. S3 객체 잠금이 활성화된 S3 버킷을 생성합니다. 버전 관리를 활성화합니다. 객체에 법적 보존을 추가합니다. 객체를 삭제해야 하는 사용자의 IAM 정책에 s3:PutObjectLegalHold 권한을 추가합니다.

https://jibinary.tistory.com/354

**Governance (가버넌스) 모드** : 권한 있으면 변경 가능
관리자 권한을 가지고 있는 사용자만 오브젝트를 업데이트 및 삭제할 수 있으며, 가버넌스 모드를 해제할 수 있다.
여기서 사용되는 권한: "s3:BypassGovernanceRetention"

정답 : D

## Q6 (pdf Q#152)
한 회사가 신입 직원 교육을 위해 3계층 웹 애플리케이션을 사용합니다. 이 애플리케이션은 매일 12시간만 접속됩니다.
회사는 정보를 저장하기 위해 Amazon RDS for MySQL DB 인스턴스를 사용하고 있으며 비용을 최소화하고자 합니다.
이러한 요구 사항을 충족하기 위해 솔루션 아키텍트는 무엇을 해야 할까요?

Amazon RDS for MySQL DB 인스턴스 비용 최소화 방법

A. AWS Systems Manager Session Manager에 대한 IAM 정책을 구성합니다. 해당 정책에 대한 IAM 역할을 생성합니다. 역할의 신뢰 관계를 업데이트합니다.
DB 인스턴스의 자동 시작 및 중지를 설정합니다.
B. DB 인스턴스가 중지되었을 때 사용자가 캐시에서 데이터에 액세스할 수 있도록 Amazon ElastiCache for Redis 캐시 클러스터를 생성합니다.
DB 인스턴스가 시작된 후 캐시를 무효화합니다.
C. Amazon EC2 인스턴스를 시작합니다. Amazon RDS에 대한 액세스 권한을 부여하는 IAM 역할을 생성합니다. EC2 인스턴스에 역할을 연결합니다.
원하는 일정에 따라 EC2 인스턴스를 시작 및 중지하는 cron 작업을 구성합니다.
D. DB 인스턴스를 시작 및 중지하는 AWS Lambda 함수를 생성합니다. Amazon EventBridge(Amazon CloudWatch Events) 예약 규칙을 생성하여 Lambda 함수를 호출합니다. Lambda 함수를 해당 규칙의 이벤트 대상으로 구성합니다.

https://sonit.tistory.com/19

AWS Lambda 함수를 사용하여 일정 시간이 지난 후에 EC2 인스턴스와 RDS 데이터베이스를 중지하고 다시 시작하는 방법
사용 시간에 따른 비용 최적화를 위해 Lambda를 사용하여 EC2 인스턴스와 RDS를 자동으로 on/off 할 수 있도록 구성
출처: https://sonit.tistory.com/19 [Son IT:티스토리]

정답 : D

## Q7(pdf Q#179)
솔루션 아키텍트는 애플리케이션이 Amazon RDS DB 인스턴스에 액세스하는 데 사용하는 데이터베이스 사용자 이름과 암호를 안전하게 저장해야 합니다.
이 데이터베이스에 액세스하는 애플리케이션은 Amazon EC2 인스턴스에서 실행됩니다. 솔루션 아키텍트는 AWS Systems Manager 파라미터 스토어에 안전한 파라미터를 생성하려고 합니다. 이 요구 사항을 충족하기 위해 솔루션 아키텍트는 무엇을 해야 할까요?

EC2가 암호화된 SecureString 파라미터를 어떻게 안전하게 읽는가

A. 파라미터 스토어 파라미터에 대한 읽기 액세스 권한이 있는 IAM 역할을 생성합니다. 파라미터를 암호화하는 데 사용되는 AWS Key Management Service(AWS KMS) 키에 대한 복호화 액세스 권한을 허용합니다.
이 IAM 역할을 EC2 인스턴스에 할당합니다.
B. 파라미터 스토어 파라미터에 대한 읽기 액세스 권한이 있는 IAM 정책을 생성합니다. 파라미터를 암호화하는 데 사용되는 AWS Key Management Service(AWS KMS) 키에 대한 복호화 액세스 권한을 허용합니다.
이 IAM 정책을 EC2 인스턴스에 할당합니다.
C. 파라미터 스토어 파라미터와 EC2 인스턴스 간에 IAM 신뢰 관계를 생성합니다.
신뢰 정책에서 Amazon RDS를 주체로 지정합니다.
D. DB 인스턴스와 EC2 인스턴스 간에 IAM 트러스트 관계를 생성합니다. 트러스트 정책에서 Systems Manager를 보안 주체로 지정합니다.

https://sw-ym.tistory.com/196

**Parameter Store 특징**
1. 설정 값은 key - value 형태로 저장
2. 데이터 저장 유형은 아래 3가지 타입
	String(일반 텍스트)
	StringList(쉼표로 구분된 문자열 리스트)
	SecureString(KMS로 암호화 된 정보)
3. 버전 관리 지원
	값이 변경될 때마다 자동으로 버전이 증가
	또한, 이전 버전 롤백 가능
4. IAM 기반 접근 제어
	Parameter별로 IAM 권한 설정하여 접근 제어 가능
	예: 특정 EC2만 읽을 수 있게 설정 가능
5. 유효기간 설정 가능
	Parameter별로 TTL(Time-to -Live) 설정 가능 (유료)

정답 : A

B가 정답이 아닌 이유 : IAM POLICY는 EC2에 직접 할당 불가능하다 -> 구조적으로 불가능함

## Q8(pdf Q#185)
한 회사가 Amazon ECS를 사용하여 애플리케이션을 실행합니다. 이 애플리케이션은 원본 이미지의 크기를 조정한 버전을 생성한 다음 Amazon S3 API를 호출하여 크기가 조정된 이미지를 Amazon S3에 저장합니다.
솔루션 아키텍트는 애플리케이션이 Amazon S3에 액세스할 수 있는 권한을 확보하려면 어떻게 해야 할까요?

Amazon S3에 액세스할 수 있는 권한을 확보하는 방법

A. AWS IAM에서 S3 역할을 업데이트하여 Amazon ECS에서 읽기/쓰기 액세스를 허용한 다음 컨테이너를 다시 시작합니다.
B. S3 권한이 있는 IAM 역할을 생성하고 작업 정의에서 해당 역할을 taskRoleArn으로 지정합니다.
C. Amazon ECS에서 Amazon S3에 대한 액세스를 허용하는 보안 그룹을 생성하고 ECS 클러스터에서 사용하는 시작 구성을 업데이트합니다.
D. S3 권한이 있는 IAM 사용자를 생성한 다음 해당 계정으로 로그인한 상태에서 ECS 클러스터용 Amazon EC2 인스턴스를 다시 시작합니다.

ECS에서 AWS 서비스 접근 방식
ECS Task → IAM Role (Task Role)

ECS는 컨테이너 단위로 권한을 부여함

taskRoleArn: 컨테이너가 AWS API(S3, DynamoDB 등)를 호출할 때 사용하는 IAM Role

정답 : B

## Q9(pdf Q#208)
한 회사가 Amazon EC2 인스턴스에서 Amazon S3 버킷으로 데이터를 이동해야 합니다. 이 회사는 API 호출이나 데이터가 공용 인터넷 경로를 통해 전송되지 않도록 해야 합니다. 또한, EC2 인스턴스만 S3 버킷에 데이터를 업로드할 수 있어야 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇일까요?


A. EC2 인스턴스가 위치한 서브넷에 Amazon S3용 인터페이스 VPC 엔드포인트를 생성합니다. S3 버킷에 리소스 정책을 연결하여
EC2 인스턴스의 IAM 역할만 액세스를 허용하도록 설정합니다.
B. EC2 인스턴스가 위치한 가용 영역에 Amazon S3용 게이트웨이 VPC 엔드포인트를 생성합니다. 적절한 보안 그룹을 엔드포인트에 연결합니다.
S3 버킷에 리소스 정책을 연결하여 EC2 인스턴스의 IAM 역할만 액세스를 허용하도록 설정합니다.
C. EC2 인스턴스 내부에서 nslookup 도구를 실행하여 S3 버킷 서비스 API 엔드포인트의 프라이빗 IP 주소를 확인합니다. VPC 라우팅 테이블에 경로를 생성하여 EC2 인스턴스가 S3 버킷에 액세스할 수 있도록 합니다. S3 버킷에 리소스 정책을 연결하여
EC2 인스턴스의 IAM 역할만 액세스를 허용하도록 설정합니다.
D. AWS에서 제공하는 공개 ip-ranges.json 파일을 사용하여 S3 버킷 서비스 API 엔드포인트의 프라이빗 IP 주소를 확인합니다. VPC 라우팅 테이블에 EC2 인스턴스가 S3 버킷에 액세스할 수 있도록 경로를 생성합니다. S3 버킷에 리소스 정책을 연결하여 EC2 인스턴스의 IAM 역할만 액세스할 수 있도록 합니다.

https://s0ng.tistory.com/m/entry/AWS-SCS-S3-VPC-%EC%97%94%EB%93%9C%ED%8F%AC%EC%9D%B8%ED%8A%B8-%EC%A0%84%EB%9E%B5

보안 구성

S3 Gateway VPC Endpoint 생성
라우팅 테이블에 자동 반영
S3 Bucket Policy
	특정 IAM Role만 허용
	필요 시 aws:sourceVpce 조건 추가 가능

요구사항 100% 충족
비용 없음 (Gateway Endpoint는 무료)

정답 : B

## Q10(pdf Q#222)
한 회사가 자사 AWS 계정에서 작업을 수행하기 위해 외부 업체를 고용했습니다. 해당 업체는 자사 소유의 AWS 계정에 호스팅된 자동화 도구를 사용합니다.
업체는 회사 AWS 계정에 대한 IAM 액세스 권한이 없습니다.
솔루션 아키텍트는 어떻게 업체에 이 액세스 권한을 부여해야 할까요?

A. 회사 계정에 IAM 역할을 생성하여 업체 IAM 역할에 액세스 권한을 위임합니다. 업체가 필요로 하는 권한에 대한 적절한 IAM 정책을 역할에 연결합니다.
B. 회사 계정에 암호 복잡성 요구 사항을 충족하는 암호를 가진 IAM 사용자를 생성합니다. 업체가 필요로 하는 권한에 대한 적절한 IAM 정책을 사용자에게 연결합니다.
C. 회사 계정에 IAM 그룹을 생성합니다. 업체 계정의 도구 IAM 사용자를 그룹에 추가합니다. 업체가 필요로 하는 권한에 대한 적절한 IAM 정책을 그룹에 연결합니다.
D. IAM 콘솔에서 공급자 유형으로 "AWS 계정"을 선택하여 새 ID 공급자를 생성합니다. 벤더의 AWS 계정 ID와 사용자 이름을 제공하세요.
벤더가 필요로 하는 권한에 대해 새 공급자에 적절한 IAM 정책을 연결하세요.

외부 업체(벤더) 를 고용
벤더는 자기 AWS 계정을 가지고 있음
벤더의 자동화 도구가 우리 회사 AWS 계정에서 작업 수행

현재: 벤더는 우리 계정에 IAM 사용자 없음

요구사항: 안전하게 IAM 접근 권한 부여

키워드
외부 AWS 계정 / 자동화 도구 / 권한 위임 / 보안 Best Practice

AWS 공식 Best Practice: Cross-Account Access
IAM Role + STS AssumeRole

구조
	회사 계정
		IAM Role 생성
		벤더가 필요로 하는 최소 권한 정책 연결
		Trust Policy에 벤더 AWS 계정 허용

	벤더 계정
		자동화 도구가 자신의 IAM Role/User로
		sts:AssumeRole 호출

	임시 자격 증명(Temporary Credentials) 로 작업 수행

장점
Access Key 공유 안 함
IAM User 생성 안 함
임시 권한 (보안 ↑)
언제든 즉시 권한 회수 가능
CloudTrail로 추적 가능

외부 계정 접근 = 무조건 IAM Role

정답 : A

## Q11(pdf Q#239)
솔루션 아키텍트는 회사의 애플리케이션을 위한 새로운 마이크로서비스를 설계해야 합니다. 클라이언트는 HTTPS 엔드포인트를 호출하여 해당 마이크로서비스에 접근할 수 있어야 합니다.
또한, 마이크로서비스는 AWS Identity and Access Management(IAM)를 사용하여 호출을 인증해야 합니다. 솔루션 아키텍트는 Go 1.x로 작성된 단일 AWS Lambda 함수를 사용하여 이 마이크로서비스의 로직을 구현할 것입니다.
다음 중 어떤 솔루션이 가장 운영 효율적인 방식으로 함수를 배포할까요?

요구사항 정리

마이크로서비스
HTTPS 엔드포인트 제공
IAM으로 호출 인증
단일 Lambda 함수 (Go 1.x)
운영 효율성 최우선 (구성 단순, 관리 부담 최소)

핵심 키워드
HTTPS + IAM 인증 + Lambda 단독 + 최소 운영 오버헤드

A. Amazon API Gateway REST API를 생성합니다. Lambda 함수를 사용하도록 메서드를 구성합니다. API에서 IAM 인증을 활성화합니다.
B. 함수에 대한 Lambda 함수 URL을 생성합니다. 인증 유형으로 AWS_IAM을 지정합니다.
C. Amazon CloudFront 배포를 생성합니다. Lambda@Edge에 함수를 배포합니다. Lambda@Edge 함수에 IAM 인증 로직을 통합합니다.
D. Amazon CloudFront 배포를 생성합니다. CloudFront Functions에 함수를 배포합니다. 인증 유형으로 AWS_IAM을 지정합니다.

Lambda Function URL이란?

Lambda에 직접 HTTPS 엔드포인트 제공
API Gateway 없이도 호출 가능
AWS_IAM 인증 지원
별도 인프라 구성 불필요

운영 효율이 가장 좋고 가장 단순하다.

정답 : B

## Q12(pdf Q#253)
솔루션 아키텍트가 Policy1과 Policy2라는 두 개의 IAM 정책을 생성했습니다. 두 정책 모두 IAM 그룹에 연결되어 있습니다. 클라우드 엔지니어가 해당 IAM 그룹에 IAM 사용자로 추가되었습니다. 클라우드 엔지니어는 어떤 작업을 수행할 수 있을까요?

A. IAM 사용자 삭제 
B. 디렉터리 삭제 
C. Amazon EC2 인스턴스 삭제 
D. Amazon CloudWatch Logs에서 로그 삭제

policy 1(allow)
IAM: 조회(List/Get)만 가능
KMS: 조회만 가능
EC2: 모든 액션 허용 (ec2:*)
Directory Service(ds): 모든 액션 허용
CloudWatch Logs: Get / Describe만 가능

policy 2 (Explicit Deny)
Directory Service(ds)의 Delete 계열 액션은 무조건 거부

정답 : C

## Q13(pdf Q#260)
한 회사의 규정 준수 팀이 파일 공유를 AWS로 이전해야 합니다. 해당 공유는 Windows Server SMB 파일 공유에서 실행됩니다. 자체 관리형 온프레미스 Active Directory가 파일 및 폴더에 대한 액세스를 제어합니다.
이 회사는 솔루션의 일부로 Amazon FSx for Windows File Server를 사용하려고 합니다. 회사는 AWS로 이전 후 온프레미스 Active Directory 그룹이 FSx for Windows File Server SMB 규정 준수 공유, 폴더 및 파일에 대한 액세스를 제한하도록 해야 합니다.
이 회사는 이미 FSx for Windows File Server 파일 시스템을 구축했습니다.
이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

기존 환경:
	Windows Server SMB 파일 공유
	온프레미스 Active Directory로 파일/폴더 접근 제어
AWS 이전:

	Amazon FSx for Windows File Server 사용
	FSx 파일 시스템은 이미 생성됨
요구사항:
	기존 온프레미스 AD 그룹이
	FSx의 SMB 공유 / 폴더 / 파일 접근을 계속 제어

A. Active Directory에 연결하는 Active Directory 커넥터를 생성합니다. Active Directory 그룹을 IAM 그룹에 매핑하여 액세스를 제한합니다.
B. '제한(Restrict)' 태그 키와 '규정 준수(Compliance)' 태그 값을 가진 태그를 할당합니다. Active Directory 그룹을 IAM 그룹에 매핑하여 액세스를 제한합니다.
C. FSx for Windows File Server에 직접 연결된 IAM 서비스 연결 역할을 생성하여 액세스를 제한합니다.
D. 접근을 제한하려면 시스템을 Active Directory에 연결하십시오.

https://docs.aws.amazon.com/ko_kr/fsx/latest/WindowsGuide/what-is.html
FSx for Windows File Server(아마존 공식 문서)

FSx for Windows File Server 핵심 개념
FSx for Windows File Server는:
	Windows 네이티브 파일 시스템
	SMB + NTFS ACL 사용
접근 제어는:
	IAM 아님
	Active Directory (Self-managed AD 또는 AWS Managed AD)
FSx를 AD에 조인(Join)해야
→ AD 사용자/그룹으로 파일 접근 제어 가능

정답 : D

## Q14(pdf Q#289)
한 회사에서 동일한 AWS 계정에 있는 Amazon S3 버킷에 대한 읽기 액세스 권한이 필요한 AWS Lambda 함수를 사용하고 있습니다.
다음 중 가장 안전한 방법으로 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

Lambda + S3 접근 + 보안 최우선

A. S3 버킷에 대한 읽기 액세스 권한을 부여하는 S3 버킷 정책을 적용합니다.
B. Lambda 함수에 IAM 역할을 적용하고, 해당 역할에 S3 버킷에 대한 읽기 액세스 권한을 부여하는 IAM 정책을 적용합니다.
C. Lambda 함수의 코드에 액세스 키와 비밀 키를 포함시켜 S3 버킷에 대한 읽기 액세스에 필요한 IAM 권한을 부여합니다.
D. Lambda 함수에 IAM 역할을 적용하고, 해당 역할에 계정 내 모든 S3 버킷에 대한 읽기 액세스 권한을 부여하는 IAM 정책을 적용합니다.

AWS 권장 방식 (Best Practice)

Lambda → IAM Role → 최소 권한 정책

Lambda는 IAM Role(Execution Role) 을 통해 AWS 서비스에 접근
Access Key를 코드에 넣지 않음
필요한 S3 버킷에 대해서만 GetObject, ListBucket 허용
자동으로 임시 자격 증명(Temporary Credentials) 사용

정답 : B

A 오답 이유 : IAM Role 없이 접근 제어
C 오답 이유 : 코드에 비밀 키 포함 -> 보안 최악
D 오답 이유 : 최소 권한 원칙 위반 -> 가장 안전한 방법은 아님

## Q15(pdf Q#387)
새로운 직원이 배포 엔지니어로 회사에 합류했습니다. 이 배포 엔지니어는 AWS CloudFormation 템플릿을 사용하여 여러 AWS 리소스를 생성할 예정입니다.
솔루션 아키텍트는 배포 엔지니어가 최소 권한 원칙을 준수하면서 업무를 수행하도록 하기를 원합니다.
솔루션 아키텍트는 이 목표를 달성하기 위해 어떤 조치를 취해야 할까요? (두 가지를 선택하세요.)

A. 배포 엔지니어가 AWS CloudFormation 스택 작업을 수행할 때 AWS 계정 루트 사용자 자격 증명을 사용하도록 합니다.
B. 배포 엔지니어를 위한 새 IAM 사용자를 생성하고, 해당 IAM 사용자를 PowerUsers IAM 정책이 적용된 그룹에 추가합니다.
C. 배포 엔지니어를 위한 새 IAM 사용자를 생성하고, 해당 IAM 사용자를 AdministratorAccess IAM 정책이 적용된 그룹에 추가합니다.
D. 배포 엔지니어를 위한 새 IAM 사용자를 생성하고, 해당 IAM 사용자를 AWS CloudFormation 작업만 허용하는 IAM 정책이 적용된 그룹에 추가합니다.
E. 배포 엔지니어가 AWS CloudFormation 스택에 특정한 권한을 명시적으로 정의하고 해당 IAM 역할을 사용하여 스택을 시작할 수 있도록 IAM 역할을 생성합니다.

배포 엔지니어에게:

cloudformation:* 또는 필요한 CloudFormation API만 허용
EC2, S3, IAM 등을 직접 조작할 권한 없음
직접 리소스 생성 권한을 주지 않고, CloudFormation을 통해서만 작업
-> 최소 권한 원칙 충족

CloudFormation의 핵심 보안 기능

구조:
배포 엔지니어: CloudFormation 실행만 가능
CloudFormation 서비스:
	지정된 IAM Role을 Assume
	그 Role에 필요한 리소스 생성 권한만 부여
AWS 공식 Best Practice

정답 : D,E

## Q16(pdf Q#403)
개발자는 AWS Lambda 함수를 사용하여 Amazon S3에 파일을 업로드하는 애플리케이션을 가지고 있으며, 해당 작업을 수행하는 데 필요한 권한이 필요합니다.
개발자는 이미 Amazon S3에 필요한 유효한 IAM 자격 증명을 가진 IAM 사용자를 보유하고 있습니다.
솔루션 아키텍트는 이 권한을 부여하기 위해 무엇을 해야 할까요?

A. Lambda 함수의 리소스 정책에 필요한 IAM 권한을 추가합니다.
B. Lambda 함수에서 기존 IAM 자격 증명을 사용하여 서명된 요청을 생성합니다.
C. 새 IAM 사용자를 생성하고 Lambda 함수에서 기존 IAM 자격 증명을 사용합니다.
D. 필요한 권한을 가진 IAM 실행 역할을 생성하고 해당 IAM 역할을 Lambda 함수에 연결합니다.

Lambda는 IAM User 자격 증명을 써야 할까?
-> 아니다. Lambda는 IAM Role을 사용해야 한다.

Lambda 권한 부여 Best Practice
Lambda → IAM Execution Role → AWS 서비스(S3)

Lambda는:
IAM User의 Access Key를 사용 
IAM Role을 Assume하여 권한 획득 

이 Role에:
s3:PutObject 등 필요한 최소 권한만 부여

정답 : D

## Q17(pdf Q#418)
솔루션 아키텍트는 팀 구성원이 서로 다른 두 AWS 계정(개발 계정과 프로덕션 계정)에 있는 Amazon S3 버킷에 액세스할 수 있도록 해야 합니다.
현재 팀은 개발 계정의 S3 버킷에 액세스할 수 있으며, 이 버킷은 해당 계정에서 적절한 권한을 가진 IAM 그룹에 할당된 고유한 IAM 사용자를 통해 접근 권한을 부여받습니다.
솔루션 아키텍트는 프로덕션 계정에 IAM 역할을 생성했습니다. 이 역할에는 프로덕션 계정의 S3 버킷에 대한 액세스 권한을 부여하는 정책이 포함되어 있습니다.
최소 권한 원칙을 준수하면서 이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

같은 팀원이 두 계정의 S3 버킷 모두 접근
최소 권한 원칙 준수

A. 개발 계정 사용자에게 관리자 액세스 정책을 연결합니다.
B. 프로덕션 계정의 역할에 대한 신뢰 정책에 개발 계정을 주체로 추가합니다.
C. 프로덕션 계정의 S3 버킷에서 "S3 공개 액세스 차단" 기능을 비활성화합니다.
D. 프로덕션 계정에 각 팀 구성원에 대해 고유한 자격 증명을 가진 사용자를 생성합니다.

AWS 권장 교차 계정 접근 방식

IAM User (Dev 계정)
-> AssumeRole (Prod 계정 IAM Role)
-> Prod S3 버킷 접근

이 구조의 장점

IAM User를 새로 만들 필요 없음
권한은 Role에만 집중 관리
최소 권한 원칙 충족
AWS 공식 Best Practice

정답 : B

## Q18(pdf Q#423)
솔루션 아키텍트가 다음 JSON 텍스트를 ID 기반 정책으로 사용하여 특정 권한을 부여하려고 합니다.
솔루션 아키텍트는 이 정책을 어떤 IAM 주체에 연결할 수 있습니까? (두 개를 선택하십시오.)

A. 역할
B. 그룹
C. 조직
D. Amazon Elastic Container Service(Amazon ECS) 리소스
E. Amazon EC2 리소스

https://jibinary.tistory.com/388

ID 기반 정책은 IAM User, IAM Group, IAM Role에 연결하는 정책이다.

AWS 계정에 속한 다수의 User, Group, Role에 독립적으로 연결할 수 있는 Policy이다. 2가지 유형의 Policy이 있다.
AWS managed policies (AWS 관리형 정책) - AWS 측에서 관리하는 Policy.
Customer managed policies (고객 관리형 정책)  - 사용자가 관리하는 Policy.

정답 : A,B

## Q19(pdf Q#428)
서버리스 애플리케이션이 Amazon API Gateway, AWS Lambda 및 Amazon DynamoDB를 사용합니다. Lambda 함수는 DynamoDB 테이블에 대한 읽기 및 쓰기 권한이 필요합니다.
다음과 같은 솔루션을 사용하면 Lambda 함수가 DynamoDB 테이블에 가장 안전하게 액세스할 수 있습니다.

Lambda가 DynamoDB에 **가장 안전하게** 접근하는 방법

A. Lambda 함수에 대한 프로그래밍 방식 액세스 권한이 있는 IAM 사용자를 생성합니다. 해당 사용자에게 DynamoDB 테이블에 대한 읽기 및 쓰기 액세스 권한을 허용하는 정책을 연결합니다.
access_key_id 및 secret_access_key 매개변수를 Lambda 환경 변수의 일부로 저장합니다. 다른 AWS 사용자가 Lambda 함수 구성에 대한 읽기 및 쓰기 액세스 권한을 갖지 않도록 합니다.
B. Lambda를 신뢰할 수 있는 서비스로 포함하는 IAM 역할을 생성합니다. 해당 역할에 DynamoDB 테이블에 대한 읽기 및 쓰기 액세스 권한을 허용하는 정책을 연결합니다.
Lambda 함수의 구성을 업데이트하여 새 역할을 실행 역할로 사용하도록 합니다.
C. Lambda 함수에 대한 프로그래밍 방식 액세스 권한이 있는 IAM 사용자를 생성합니다. 해당 사용자에게 DynamoDB 테이블에 대한 읽기 및 쓰기 액세스 권한을 허용하는 정책을 연결합니다.
access_key_id 및 secret_access_key 매개변수를 AWS Systems Manager 파라미터 스토어에 보안 문자열로 저장합니다.
Lambda 함수 코드를 업데이트하여 DynamoDB 테이블에 연결하기 전에 보안 문자열 매개변수를 검색하도록 합니다.
D. DynamoDB를 신뢰할 수 있는 서비스로 포함하는 IAM 역할을 생성합니다. 해당 역할에 Lambda 함수에서 읽기 및 쓰기 액세스를 허용하는 정책을 연결합니다.
Lambda 함수의 코드를 수정하여 새 역할에 실행 역할로 연결되도록 합니다.

Lambda가 AWS 리소스에 접근하는 정석적인 방법

-> IAM 실행 역할 (Execution Role)

Lambda 함수에는 IAM Role을 직접 연결할 수 있음
Lambda는 이 역할을 자동으로 Assume
코드 안에 Access Key / Secret Key 절대 저장 
AWS에서 가장 권장하고 안전한 방식

Lambda → 다른 AWS 서비스 접근
	IAM Role (Execution Role)
	Access Key 절대 사용 

Lambda가 DynamoDB에 가장 안전하게 접근하는 방법은
IAM 실행 역할(Role)을 생성하여 Lambda에 연결하는 것이다.

정답 : B

## Q20(pdf Q#455)
한 회사가 AWS Organizations를 사용하고 있습니다. 이 회사는 일부 AWS 계정에 대해 서로 다른 예산을 설정하여 운영하려고 합니다. 또한, 특정 기간 동안 할당된 예산 임계값에 도달하면 알림을 받고 AWS 계정에 추가 리소스가 프로비저닝되는 것을 자동으로 방지하려고 합니다.
다음과 같은 기능을 구현할 수 있는 솔루션 조합은 무엇입니까? (세 가지를 선택하십시오.)

A. AWS Budgets를 사용하여 예산을 생성합니다. 필요한 AWS 계정의 비용 및 사용량 보고서 섹션에서 예산 금액을 설정합니다.
B. AWS Budgets를 사용하여 예산을 생성합니다. 필요한 AWS 계정의 청구 대시보드에서 예산 금액을 설정합니다.
C. 필요한 권한을 가진 AWS Budgets용 IAM 사용자를 생성하여 예산 작업을 실행합니다.
D. 필요한 권한을 가진 AWS Budgets용 IAM 역할을 생성하여 예산 작업을 실행합니다.
E. 각 계정이 예산 임계값에 도달하면 회사에 알림을 보내는 경고를 추가합니다. 적절한 구성 규칙으로 생성된 IAM ID를 선택하여 추가 리소스 프로비저닝을 방지하는 예산 작업을 추가합니다.
F. 각 계정이 예산 임계값에 도달하면 회사에 알림을 보내는 경고를 추가합니다. 추가 리소스 프로비저닝을 방지하기 위해 적절한 서비스 제어 정책(SCP)으로 생성된 IAM ID를 선택하는 예산 작업을 추가합니다.

AWS Budgets를 사용하여 예산 생성 (청구 대시보드)

AWS Budgets는 Billing 콘솔(청구 대시보드) 에서 설정
계정별, OU별 예산 설정 가능
예산 설정의 올바른 위치

AWS Budgets용 IAM 역할 생성

Budget Actions는 IAM Role을 사용해 자동 작업 실행
예산 임계값 도달 시:
SCP 적용
IAM 정책 적용
특정 작업 차단
IAM User ❌, Role ⭕

SCP를 사용하는 Budget Action

요구사항 핵심:
	“AWS 계정에 추가 리소스가 프로비저닝되는 것을 자동으로 방지”
가장 강력하고 조직 차원의 차단 수단 = Service Control Policy (SCP)
Budget 임계값 도달 시:
	SCP 적용
	ec2:RunInstances, rds:CreateDBInstance 등 차단
✔ AWS Organizations 환경에 최적

정답 : B,D,F

오답 정리
A	예산은 Cost & Usage Report에서 설정 ❌
C	자동 작업은 IAM User ❌, Role ⭕
E	IAM 기반 차단은 조직 전체 통제 불가

## Q21(pdf Q#476)
한 회사가 가까운 미래에 급속한 성장을 예상하고 있습니다. 솔루션 아키텍트는 기존 사용자를 구성하고 AWS에서 새 사용자에게 권한을 부여해야 합니다. 솔루션 아키텍트는 IAM 그룹을 생성하기로 결정했습니다. 솔루션 아키텍트는 부서를 기준으로 새 사용자를 IAM 그룹에 추가할 것입니다.
새 사용자에게 권한을 부여하는 가장 안전한 추가 조치는 무엇입니까?

권한을 어디에, 어떻게 부여하는가

A. 서비스 제어 정책(SCP)을 적용하여 액세스 권한을 관리합니다.
B. 최소 권한 권한을 가진 IAM 역할을 생성하고 해당 역할을 IAM 그룹에 연결합니다.
C. 최소 권한 권한을 부여하는 IAM 정책을 생성하고 해당 정책을 IAM 그룹에 연결합니다.
D. IAM 역할을 생성하고 최대 권한을 정의하는 권한 경계를 역할과 연결합니다.

IAM 그룹의 역할

IAM 그룹은 권한을 직접 갖지 않음
그룹에 IAM 정책을 연결
사용자는 그룹에 추가됨으로써 권한을 상속
-> 따라서 권한 관리의 핵심은 “정책”

최소 권한 원칙(Least Privilege) 충족
부서별 그룹 + 필요한 권한만 담은 정책
신규 사용자 추가 시:
	그룹에만 추가하면 끝
	권한 과다 부여 위험 최소화
AWS IAM의 정석적인 운영 방식

정답 : C

## Q22(pdf Q#484)
한 회사가 여러 개의 개별 AWS 계정에서 통합된 멀티 계정 아키텍처로 전환하려고 합니다. 이 회사는 여러 사업부를 위해 새로운 AWS 계정을 여러 개 생성할 계획입니다.
이러한 AWS 계정에 대한 액세스는 중앙 집중식 기업 디렉터리 서비스를 사용하여 인증해야 합니다.
솔루션 아키텍트는 이러한 요구 사항을 충족하기 위해 어떤 조치 조합을 권장해야 할까요? (두 가지를 선택하세요.)

A. 모든 기능을 활성화한 상태로 AWS Organizations에 새 조직을 생성합니다. 해당 조직에 새 AWS 계정을 생성합니다.
B. Amazon Cognito ID 풀을 설정합니다. AWS IAM Identity Center(AWS Single Sign-On)에서 Amazon Cognito 인증을 허용하도록 구성합니다.
C. AWS 계정을 관리하는 서비스 제어 정책(SCP)을 구성합니다. AWS Directory Service에 AWS IAM Identity Center(AWS Single Sign-On)를 추가합니다.
D. AWS Organizations에 새 조직을 생성합니다. 해당 조직의 인증 메커니즘이 AWS Directory Service를 직접 사용하도록 구성합니다.
E. 조직에 AWS IAM Identity Center(AWS Single Sign-On)를 설정합니다. IAM Identity Center를 구성하고 회사 디렉터리 서비스와 통합합니다.

전체 아키텍처 흐름

1. AWS Organizations 생성 (All features enabled)
2. 사업부별 AWS 계정 생성
3. IAM Identity Center 활성화
4. 기업 디렉터리(AD / IdP) 연동
5. 사용자는 SSO로 여러 계정 접근

멀티 계정 + 중앙 인증 =
AWS Organizations + IAM Identity Center(SSO)

정답 :

A. 모든 기능을 활성화한 상태로 AWS Organizations에 새 조직 생성

멀티 계정 아키텍처의 기본 전제
여러 사업부용 AWS 계정을 중앙에서 생성 및 관리
SCP, 통합 결제, 계정 관리 가능
✔ 멀티 계정 구조의 필수 구성 요소

E. 조직에 AWS IAM Identity Center 설정 + 회사 디렉터리와 통합
IAM Identity Center(구 AWS SSO)는:
	여러 AWS 계정에 대한 중앙 로그인 허브
	온프레미스 AD / AWS Managed Microsoft AD / 외부 IdP 연동 가능
사용자 인증을 기업 디렉터리에서 수행
✔ 문제의 핵심 요구사항을 정확히 충족

## Q23(pdf Q#503)
한 회사가 인프라 모니터링 서비스를 운영하고 있습니다. 이 회사는 고객의 AWS 계정 데이터를 모니터링할 수 있는 새로운 기능을 개발 중입니다.
이 새로운 기능은 고객 계정의 AWS API를 호출하여 Amazon EC2 인스턴스를 설명하고 Amazon CloudWatch 메트릭을 읽습니다.
회사가 고객 계정에 가장 안전한 방식으로 접근 권한을 얻으려면 어떻게 해야 할까요?

A. 고객이 자신의 계정에 읽기 전용 EC2 및 CloudWatch 권한과 회사 계정에 대한 신뢰 정책을 가진 IAM 역할을 생성하도록 합니다.
B. 읽기 전용 EC2 및 CloudWatch 권한을 가진 역할에 대한 임시 AWS 자격 증명을 제공하는 토큰 발급기를 구현하는 서버리스 API를 생성합니다.
C. 고객이 자신의 계정에 읽기 전용 EC2 및 CloudWatch 권한을 가진 IAM 사용자를 생성하도록 합니다. 고객의 액세스 키와 비밀 키를 암호화하여 비밀 관리 시스템에 저장합니다.
D. 고객이 자신의 계정에 읽기 전용 EC2 및 CloudWatch 권한을 가진 IAM 역할을 사용할 수 있는 Amazon Cognito 사용자를 생성하도록 합니다. Amazon Cognito 사용자 이름과 비밀번호를 암호화하여 보안 관리 시스템에 저장하십시오.

고객 계정

IAM Role (ReadOnly EC2 + CloudWatch)
Trust policy → Company AWS Account

회사 계정

sts:AssumeRole → Temporary credentials
→ EC2 Describe / CloudWatch GetMetricData

외부 회사가 고객 AWS 계정에 접근할 때
가장 안전한 방법은
Cross-account IAM Role을 AssumeRole 하는 것이다.


외부 업체 / SaaS / 모니터링 서비스
-> IAM Role + Trust Policy

“가장 안전한 방식”
-> No Access Key, Use STS

정답 : A

Cross-account IAM Role (AssumeRole)

AWS에서 가장 권장되는 외부 계정 접근 방식
	고객 계정에:
		읽기 전용 권한 IAM Role 생성
		Trust Policy에 회사 AWS 계정을 명시
	회사는:
		sts:AssumeRole로 임시 자격 증명 사용
	Access Key 저장 ❌
	최소 권한
	고객이 완전한 제어권 유지
