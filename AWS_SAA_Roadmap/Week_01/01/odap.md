3 17 89 96 109 152 179 185 208 222 239 253 260 289 387 403 418 419 423 428 429 455 476 477 484 494  503 521 556 640 675

# 17 정답 : A 
AWS에서 EC2 인스턴스가 S3와 같은 다른 AWS 서비스에 안전하게 접근하도록 설정할 때의 표준 방식은 **IAM Role(역할)**을 사용하는 것입니다.

A가 정답인 이유 (IAM Role): * EC2 인스턴스에 직접 자격 증명(Access Key/Secret Key)을 저장하지 않고도 권한을 부여할 수 있는 가장 안전한 방법입니다.

Instance Profile을 통해 역할이 인스턴스에 연결되면, 인스턴스 내의 애플리케이션은 AWS SDK 등을 통해 자동으로 임시 보안 자격 증명을 획득하여 S3에 접근합니다.

B가 오답인 이유 (IAM Policy):

정책(Policy)은 권한 정의서일 뿐입니다. 정책 자체를 EC2 인스턴스에 직접 '연결'할 수는 없으며, 반드시 Role에 정책을 연결한 뒤 그 Role을 인스턴스에 부여해야 합니다.

C, D가 오답인 이유:

IAM Group이나 IAM User는 인스턴스(서버)가 아닌 실제 사용자나 사람의 그룹을 위해 설계된 개념입니다.

사용자(User)의 자격 증명을 서버에 하드코딩하는 방식은 보안상 매우 위험하므로 권장되지 않습니다.


# 37 정답 : B 

A (Serial Console): 주로 부팅 문제나 네트워크 설정 오류 등 시스템 문제 해결용

B - 적절한 IAM 맞지 않나? 

C - SSH key 는 원격 접속용 

D - VPN 은 가상 네트워크 


# 89  정답 : A 

A 랑 B 가 헷갈림 

A : Versioning을 켜면 누가 DeleteObject를 해도 “완전 삭제”가 아니라 삭제 마커(delete marker) 가 붙고, 이전 버전이 남아서 복구 가능

여기에 MFA Delete까지 켜면, 버전 영구 삭제(특정 버전 삭제)나 버전닝 상태 변경 같은 치명적인 작업에 MFA가 필수라서 실수/오작동/권한 남용을 한 단계 더 막아줌.

B : IAM 사용자에 MFA를 켠다고 해서 S3 삭제가 자동으로 막히는 게 아님. 사용자가 권한이 있으면 MFA 로그인 상태로도 삭제는 그냥 가능해. (즉 “삭제 방지/복구” 요구에 직접 대응 못 함)


# 96 정답 : C 

A : 두 번째에 의해 us-east-1 이외의 리전에서는 모든 EC2 작업이 거부.

B: 정책의 Condition은 사용자의 소스 IP를 체크하는 것이지, 종료하려는 대상 EC2 인스턴스의 IP를 체크하는 것이 아님.

D: C와 반대되는 내용이므로 오답.


# 152 

B는 절대 아님 

C도 아닌거 같고 a 아님 d 

근데 D가 비용상 좀 더 저렴하지 않을까

A: Systems Manager Session Manager/IAM Trust 관계는 RDS 시작/중지 스케줄링이랑 무관(불필요하게 꼬아놓은 선택지).

B: ElastiCache는 비용이 추가로 들고, DB를 꺼둔 동안 “캐시로 운영”은 데이터 일관성/쓰기 처리가 애매해서 요구사항(훈련 앱 + 비용 최소화)에 안 맞음.

C: EC2를 시작/중지해봤자 RDS 비용은 그대로라서 목표(“DB 비용 최소화”)를 못 맞춤.


# 179

정답 : A 

EC2에 IAM Role(Instance Profile) 을 붙여서 ssm:GetParameter(또는 GetParameters, GetParameterHistory) 권한

(SecureString이면) 해당 파라미터를 암호화한 KMS 키에 대한 kms:Decrypt 권한을 줘야함


# 185 

B 아님 D 같은데 

정답 : B 

ECS에서 컨테이너(애플리케이션)가 AWS API(S3)에 접근하려면 Task Role(IAM Role for Tasks) 를 써야 해요.
즉, S3 권한이 붙은 IAM Role을 만들고 ECS task definition의 taskRoleArn 에 지정하면 컨테이너가 그 역할 권한으로 S3 API 호출을 합니다.

왜 D는 오답?

IAM 사용자를 만들어 EC2에 “로그인한 계정”으로 권한을 준다는 개념은 AWS 권한 모델이 아님.

EC2에 붙는 건 IAM Role(인스턴스 프로파일) 이고, ECS에선 더 올바른 방식이 Task Role.

# 208 

정답: B

S3 API 호출/데이터가 퍼블릭 인터넷 경로(IGW/NAT)로 나가면 안 됨
→ Amazon S3는 VPC Endpoint 중에서 “Gateway Endpoint”가 정석(라우트 테이블에 S3 프리픽스 경로가 생겨서 사설로 감).

업로드 권한은 오직 그 EC2만
→ S3 버킷 정책에서 EC2에 붙은 IAM Role만 허용(원칙적으로 그 Role을 가진 엔티티만 접근 가능).


# 222 

정답 B ,C 아님 

정답 : A 

IAM Group에는 다른 계정의 IAM user를 추가할 수 없음 (그룹은 계정 내부 사용자만)

회사 계정에 IAM Role 생성

그 Role의 Trust policy(AssumeRole 허용 대상) 를 벤더 계정의 IAM Role(또는 특정 Principal) 로 설정

# 239 는 생략


# 253 정답 : B 

# 289 정답 : B 

# 387 

이거는 선지가 5개네요 

정답 : D , E 


D: 배포 엔지니어용 IAM 사용자를 만들고, 그 사용자는 CloudFormation 관련 작업(스택 생성/업데이트/삭제/조회 등)만 할 수 있게 제한.

E: 실제로 스택이 만들 리소스 권한은 별도의 IAM Role로 명확히 정의하고(최소 권한), 스택 실행 시 그 Role을 사용하게 함(= CloudFormation이 그 Role 권한으로 리소스 생성).


# 403 

이미 IAM 계정 보유 

정답: D

Lambda가 S3에 업로드하려면 Lambda 실행 역할(Execution Role) 에 S3 권한을 붙여서 Lambda에 연결해야 함.