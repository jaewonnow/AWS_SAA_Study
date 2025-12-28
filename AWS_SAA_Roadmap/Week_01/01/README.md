# IAM 이란?
> Identity and Access Management(IAM)는 AWS 리소스의 보안과 접근 제어를 관리


# IAM USER
> 실제 물리적 사용자와 매핑
비밀번호 : 각 user 는 AWS Console 비밀번호를 가짐

# IAM Group
> IAM USER 를 IAM Group 으로 묶어 관리할 수 있다
그룹에 대한 권한을 설명하는 정책을 할당

# IAM Role
> IAM User 나 IAM Group 에 부여할 권한(Role)을 정의하는 JSON 문서 사용
EC2 인스턴스나 다른 AWS 서비스에 대한 권한을 부여할 때 사용

# Policy

> MFA : 사용자의 보안을 강화하기 위해 MFA 를 활성화할수 있다.
ex) Google Authenticator


# CLI , SDK

- CLI 사용 : 명령줄 인터페이스를 통해 AWS 서비스 관리
- SDK 사용 : 프로그래밍 언어를 사용하여 AWS 관리
- Access Key 사용 : AWS 에 접글할 수 있는 Access  키 생성 

---

## 1) IAM의 “결론”

- Authentication(누구냐): User / Role(+AssumeRole)

- Authorization(뭘 할 수 있냐): Policy

- 권한은 기본적으로 Deny(명시 Allow가 있어야 가능)

## 2) Policy가 실제로 어떻게 적용되는지

- Identity-based policy: User/Group/Role에 붙는 정책(가장 흔함)

- Resource-based policy: 리소스에 붙는 정책 (예: S3 Bucket Policy, KMS Key policy, SQS, SNS 등)

- (시험 자주) Explicit Deny가 최우선이고, 그 다음 Allow, 나머지는 암묵적 Deny

그리고 Policy 구조는 최소로 이것만 기억

- Effect (Allow/Deny)

- Action (무슨 API)

- Resource (어떤 리소스 ARN)

- Condition (언제/어떤 조건에서)

## 3) User / Group / Role 차이를 시험 관점으로 한 줄로

- User: 사람(또는 장기 자격증명 필요할 때)

- Group: 사용자 묶음(“권한은 그룹에 붙이고 유저는 그룹에 넣는다”가 정석)

- Role: 임시 자격증명(temporary credentials) 기반, AWS 서비스/외부 계정/연동에 쓰는 “모자”


## 4) Access Key에 대해 더 정확히

Access Key = Console 로그인용 아님

- 프로그래밍용(CLI/SDK/API) 장기 자격증명

유출 위험 때문에 가능하면 Role/STS로 대체(특히 EC2/Lambda/ECS)

## 5) AssumeRole / STS를 한 문장으로 정리

AssumeRole = STS로 Role을 ‘빌려서’ 임시 자격증명(AccessKeyId/Secret/SessionToken)을 받는 것

그래서 “EC2가 S3 접근해야 함” → **EC2 Instance Profile(Role)**이 정답

## 6) “이것도 시험에 많이 나옴” 체크리스트

- Root account는 Access Key 만들지 말고 MFA 필수

- IAM 정책은 최소권한(least privilege)

- Password Policy(길이/만료/재사용 금지 등) 설정 가능

- IAM은 글로벌 서비스 (Region 아님)

- (고급이지만 빈출) Permission Boundary, SCP(Organizations): “아무리 IAM Allow라도 조직 SCP에서 막으면 끝”

- Policy는 “권한(Authorization)”이고, Role은 “임시 자격증명(AssumeRole/STS)으로 권한을 쓰는 방식”

- CLI/SDK는 Access Key도 가능하지만, AWS 리소스 내부에서는 Role이 표준

- Explicit Deny > Allow > Implicit Deny


엔지니어는 CF만 조작” + “리소스 생성 권한은 역할로 분리”가 최소권한의 정석

1) 사람(엔지니어)에게는 “로그인 주체”가 필요함

AWS 콘솔/CLI로 작업하려면 Identity가 있어야 하니까
보통은

IAM Identity Center(SSO) 로 사번 계정 연동(가장 흔해지는 추세)

또는 (SSO 못 쓰면) IAM User를 만들어서 MFA 강제
이 둘 중 하나가 “사람 계정” 역할을 해.

2) 실제 권한은 “Role로 분리”하는 게 더 흔함

엔지니어가 직접 모든 권한을 갖는 게 아니라,

엔지니어는 AssumeRole 해서 필요한 작업만 하게 함.
(예: CFN-Deploy-Role, Prod-ReadOnly-Role 같은 식)

3) CloudFormation은 특히 Role 분리가 정석

엔지니어 권한: “스택 만들기/업데이트/삭제/조회” 정도만

스택이 리소스 생성할 권한: CloudFormation service role로 따로
→ 이렇게 해야 “사람 권한 과대 부여”를 피할 수 있음.