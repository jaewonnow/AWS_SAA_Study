# Placeholder
## Q1(pdf Q#52)
한 회사가 온프레미스 애플리케이션을 AWS로 마이그레이션하려고 합니다. 이 애플리케이션은 수십 기가바이트에서 수백 테라바이트에 이르는 다양한 크기의 출력 파일을 생성합니다.
애플리케이션 데이터는 표준 파일 시스템 구조에 저장되어야 합니다. 회사는 자동 확장이 가능하고, 고가용성을 제공하며, 운영 오버헤드가 최소화된 솔루션을 원합니다.
다음과 같은 요구 사항을 충족하는 솔루션은 무엇일까요?

A. 애플리케이션을 Amazon Elastic Container Service(Amazon ECS)에서 컨테이너로 실행되도록 마이그레이션합니다. 스토리지로는 Amazon S3를 사용합니다.
B. 애플리케이션을 Amazon Elastic Kubernetes Service(Amazon EKS)에서 컨테이너로 실행되도록 마이그레이션합니다. 스토리지로는 Amazon Elastic Block Store(Amazon EBS)를 사용합니다.
C. 애플리케이션을 다중 가용 영역(Multi-AZ) 자동 스케일링 그룹의 Amazon EC2 인스턴스로 마이그레이션합니다. 스토리지로는 Amazon Elastic File System(Amazon EFS)을 사용합니다.
D. 애플리케이션을 다중 가용 영역(Multi-AZ) 자동 스케일링 그룹의 Amazon EC2 인스턴스로 마이그레이션합니다. 스토리지로는 Amazon Elastic Block Store(Amazon EBS)를 사용하세요.

amazon EFS 장점 : 
완전 관리형 nfs(컴퓨터 네트워킹에서 네트워크 파일 시스템)파일 시스템
수백 TB 단위 자동 확장
여러 EC2 인스턴스에서 동시에 마운트 가능

EC2 + ASG : 
오토스케일링 가능
고가용성 확보

운영 오버헤드 최소

정답 : C

## Q2(pdf Q#221)
한 회사가 Amazon Linux EC2 인스턴스 그룹에서 애플리케이션을 실행합니다. 규정 준수를 위해 회사는 모든 애플리케이션 로그 파일을 7년 동안 보관해야 합니다.
이 로그 파일은 모든 파일에 동시에 액세스할 수 있어야 하는 보고 도구에서 분석됩니다.
이러한 요구 사항을 가장 비용 효율적으로 충족하는 스토리지 솔루션은 무엇입니까?

A. Amazon Elastic Block Store (Amazon EBS)
B. Amazon Elastic File System (Amazon EFS)
C. Amazon EC2 인스턴스 스토어
D. Amazon S3

EFS : 비용이 비싸다는 단점 존재

Amazon S3 장점 :
가장 저렴한 스토리지
동시접근 여러 애플리케이션 동시에 객체 접근 가능
내구성 높음

정답 : D

## Q3(pdf Q#252)
솔루션 아키텍트는 고객 사례 파일을 저장할 시스템을 설계해야 합니다. 이 파일들은 회사의 핵심 자산이며 매우 중요합니다. 파일 수는 시간이 지남에 따라 증가할 것입니다.
이 파일들은 Amazon EC2 인스턴스에서 실행되는 여러 애플리케이션 서버에서 동시에 액세스할 수 있어야 합니다. 또한 솔루션에는 내장된
이중화 기능이 있어야 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

A. Amazon Elastic File System (Amazon EFS)
B. Amazon Elastic Block Store (Amazon EBS)
C. Amazon S3 Glacier Deep Archive
D. AWS Backup

파일 저장, 파일 확장성 가능, EC2 동시 접근 

정답 : A

## Q4(pdf Q#1)
한 회사가 여러 대륙에 걸쳐 있는 도시들의 온도, 습도, 기압 데이터를 수집합니다. 각 사이트에서 매일 수집하는 데이터의 평균 용량은 500GB입니다.
각 사이트는 고속 인터넷 연결을 갖추고 있습니다.
이 회사는 전 세계 모든 사이트의 데이터를 가능한 한 빨리 단일 Amazon S3 버킷에 통합하고자 합니다. 솔루션은 운영 복잡성을 최소화해야 합니다.
다음 중 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

A. 대상 S3 버킷에서 S3 전송 가속을 활성화합니다. 멀티파트 업로드를 사용하여 사이트 데이터를 대상 S3 버킷에 직접 업로드합니다.
B. 각 사이트의 데이터를 가장 가까운 리전의 S3 버킷에 업로드합니다. S3 교차 리전 복제를 사용하여 객체를 대상 S3 버킷으로 복사합니다.
그 후 원본 S3 버킷에서 데이터를 삭제합니다.
C. AWS Snowball Edge Storage Optimized 디바이스 작업을 매일 예약하여 각 사이트의 데이터를 가장 가까운 리전으로 전송합니다. S3 교차 리전 복제를 사용하여 객체를 대상 S3 버킷으로 복사합니다.
D. 각 사이트의 데이터를 가장 가까운 리전의 Amazon EC2 인스턴스에 업로드합니다. 데이터를 Amazon Elastic Block Store(Amazon EBS) 볼륨에 저장합니다.
EBS 볼륨에 저장한 데이터를 정기적으로 스냅샷을 생성하고 대상 S3 버킷이 있는 리전으로 복사합니다. 해당 리전에서 EBS 볼륨을 복원합니다.

S3 Transfer Acceleration : 전세계 어이서든 가장 가까운 aws edge location으로 업로드
대용량 업로드 최적화
운영 단순 -> 빠르게 + 단순하게에 최적화

정답 : A

## Q5(pdf Q#3)
한 회사가 AWS Organizations를 사용하여 여러 부서의 AWS 계정을 관리합니다. 관리 계정에는 프로젝트 보고서가 저장된 Amazon S3 버킷이 있습니다.
이 회사는 AWS Organizations 내 조직 계정 사용자만 이 S3 버킷에 접근할 수 있도록 제한하고자 합니다.

다음 중 운영 오버헤드를 최소화하면서 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

A. 조직 ID를 참조하는 aws:PrincipalOrgID 전역 조건 키를 S3 버킷 정책에 추가합니다.
B. 각 부서별로 조직 단위(OU)를 생성합니다. aws:PrincipalOrgPaths 전역 조건 키를 S3 버킷 정책에 추가합니다.
C. AWS CloudTrail을 사용하여 CreateAccount, InviteAccountToOrganization, LeaveOrganization 및 RemoveAccountFromOrganization 이벤트를 모니터링합니다.
이벤트에 따라 S3 버킷 정책을 업데이트합니다.
D. S3 버킷에 접근해야 하는 각 사용자에게 태그를 지정합니다. aws:PrincipalTag 전역 조건 키를 S3 버킷 정책에 추가합니다.

정답 : A

aws:PrincipalOrgID : 요청 주제가 속한 조직 ID기준, 조직에 속한 모든 계정 자동 허용
내부 계정만 허용 + 최소 관리
1주차에 추가 정리 되어 있음

## Q6(pdf Q#5)
한 회사가 AWS에서 웹 애플리케이션을 호스팅하고 있으며, 사용자가 업로드한 문서를 Amazon EBS 볼륨에 저장하는 단일 Amazon EC2 인스턴스를 사용하고 있습니다.
확장성과 가용성을 향상시키기 위해 회사는 아키텍처를 복제하여 다른 가용 영역에 두 번째 EC2 인스턴스와 EBS 볼륨을 생성하고, 둘 다 애플리케이션 로드 밸런서 뒤에 배치했습니다.
이 변경을 완료한 후, 사용자들은 웹사이트를 새로 고칠 때마다 문서의 일부만 볼 수 있고 모든 문서를 동시에 볼 수 없다고 보고했습니다.
사용자가 모든 문서를 한 번에 볼 수 있도록 하려면 솔루션 아키텍트는 어떤 해결책을 제시해야 할까요?

A. 두 EBS 볼륨 모두에 모든 문서가 포함되도록 데이터를 복사합니다.
B. 애플리케이션 로드 밸런서를 구성하여 사용자를 문서가 있는 서버로 연결합니다.
C. 두 EBS 볼륨의 데이터를 Amazon EFS로 복사합니다. 새 문서를 Amazon EFS에 저장하도록 애플리케이션을 수정합니다.
D. 애플리케이션 로드 밸런서를 구성하여 두 서버 모두에 요청을 보냅니다. 각 문서는 올바른 서버에서 반환합니다.

EFS 여러 EC2인스턴스 에서 동시 마운트
완전 관리형

모든 문서를 하나의 공유 파일 시스템에 저장 가능함

-> 웹 서버 스케일아웃의 기본 패턴

정답 : C
## Q7(pdf Q#6)
한 회사가 NFS를 사용하여 사내 네트워크 연결 스토리지(NAS)에 대용량 비디오 파일을 저장합니다. 각 비디오 파일의 크기는 1MB에서 500GB까지 다양합니다.
총 스토리지 용량은 70TB이며 더 이상 증가하지 않습니다. 이 회사는 비디오 파일을 Amazon S3로 마이그레이션하기로 결정했습니다. 회사는 가능한 한 빨리, 그리고 최소한의 네트워크 대역폭을 사용하여 비디오 파일을 마이그레이션해야 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

A. Create an S3 bucket. Create an IAM role that has permissions to write to the S3 bucket. Use the AWS CLI to copy all les locally to the S3 bucket. 
B. Create an AWS Snowball Edge job. Receive a Snowball Edge device on premises. Use the Snowball Edge client to transfer data to the device. Return the device so that AWS can import the data into Amazon S3. 
C. Deploy an S3 File Gateway on premises. Create a public service endpoint to connect to the S3 File Gateway. Create an S3 bucket. Create a new NFS le share on the S3 File Gateway. Point the new le share to the S3 bucket. Transfer the data from the existing NFS le share to the S3 File Gateway. 
D. Set up an AWS Direct Connect connection between the on-premises network and AWS. Deploy an S3 File Gateway on premises. Create a public virtual interface (VIF) to connect to the S3 File Gateway. Create an S3 bucket. Create a new NFS le share on the S3 File Gateway. Point the new le share to the S3 bucket. Transfer the data from the existing NFS le share to the S3 File Gateway.

aws snowball edge
오프라인 데이터 전송
네트워크 거의 사용 안함
대용량에 최적
한번 옮기고 끝(데이터 증가 거의 없음)
-> 문제 조건을 거의 그대로 만족

대용량 데이터 마이그레이션 + 네트워크 최소 사용
-> aws snowball

정답 : B

## Q8(pdf Q#9)
한 회사가 데이터 센터에서 SMB 파일 서버를 운영하고 있습니다. 이 파일 서버에는 대용량 파일이 저장되며, 파일 생성 후 처음 며칠 동안은 자주 액세스됩니다.
7일이 지나면 파일 액세스 빈도가 매우 낮아집니다.
총 데이터 크기가 증가하고 있으며, 회사의 총 스토리지 용량에 거의 도달했습니다. 솔루션 아키텍트는 가장 최근에 액세스된 파일에 대한 저지연 액세스를 유지하면서 회사의 가용 스토리지 공간을 늘려야 합니다. 또한 향후 스토리지 문제를 방지하기 위해 파일 수명 주기 관리를 제공해야 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

A. AWS DataSync를 사용하여 7일 이상 된 데이터를 SMB 파일 서버에서 AWS로 복사합니다.
B. Amazon S3 File Gateway를 생성하여 회사의 스토리지 공간을 확장합니다. 7일 후 데이터를 S3 Glacier Deep Archive로 전환하는 S3 수명 주기 정책을 생성합니다.
C. Amazon FSx for Windows File Server 파일 시스템을 생성하여 회사의 스토리지 공간을 확장합니다.
D. 각 사용자의 컴퓨터에 Amazon S3에 접근할 수 있는 유틸리티를 설치합니다. 7일 후 데이터를 S3 Glacier Flexible로 이전하는 S3 수명주기 정책을 생성합니다.

Amazon S3 File Gateway
자주 쓰는 파일은 로컬 캐시 -> 저지연
오래된 파일은 자동으로 S3로 이동

S3 lifecycle 정책
7일 후 : S3 standard -> S3 glacier deep archive
스토리지 비용 최소화
자동관리 : 운영 부담 없음

정답 : B
## Q9(pdf Q#12)
한 글로벌 기업이 애플리케이션 로드 밸런서(ALB) 뒤의 Amazon EC2 인스턴스에 웹 애플리케이션을 호스팅하고 있습니다. 웹 애플리케이션에는 정적 데이터와 동적 데이터가 포함되어 있습니다. 이 회사는 정적 데이터를 Amazon S3 버킷에 저장합니다. 이 회사는 정적 데이터와 동적 데이터의 성능을 향상시키고 지연 시간을 줄이고자 합니다. 또한 Amazon Route 53에 등록된 자체 도메인 이름을 사용하고 있습니다.
솔루션 아키텍트는 이러한 요구 사항을 충족하기 위해 무엇을 해야 할까요?

A. S3 버킷과 ALB를 오리진으로 하는 Amazon CloudFront 배포를 생성합니다. Route 53을 구성하여 트래픽을 CloudFront 배포로 라우팅합니다.
B. ALB를 오리진으로 하는 Amazon CloudFront 배포를 생성합니다. S3 버킷을 엔드포인트로 하는 AWS Global Accelerator 표준 가속기를 생성합니다. Route 53을 구성하여 트래픽을 CloudFront 배포로 라우팅합니다.
C. S3 버킷을 오리진으로 하는 Amazon CloudFront 배포를 생성합니다. ALB와 CloudFront 배포를 엔드포인트로 하는 AWS Global Accelerator 표준 가속기를 생성합니다. 가속기 DNS 이름을 가리키는 사용자 지정 도메인 이름을 생성합니다. 웹 애플리케이션의 엔드포인트로 사용자 지정 도메인 이름을 사용합니다.
D. ALB를 오리진으로 하는 Amazon CloudFront 배포를 생성합니다. S3 버킷을 엔드포인트로 하는 AWS Global Accelerator 표준 가속기를 생성합니다. 두 개의 도메인 이름을 생성합니다. 하나의 도메인 이름은 동적 콘텐츠용 CloudFront DNS 이름으로 연결하고, 다른 도메인 이름은 정적 콘텐츠용 액셀러레이터 DNS 이름으로 연결합니다. 이러한 도메인 이름을 웹 애플리케이션의 엔드포인트로 사용합니다.

cloudfront 멀티 오리진
정적 -> S3
동적 -> ALB
CloudFront 엣지 로케이션에서
    정적 콘텐츠 캐싱
    동적 콘텐츠도 지연 최소화

정답 : A
## Q10(pdf Q#20)
한 회사가 동일한 AWS 리전의 테스트 환경으로 대량의 프로덕션 데이터를 복제하는 기능을 개선하고자 합니다. 데이터는 Amazon EBS(Amazon Elastic Block Store) 볼륨의 Amazon EC2 인스턴스에 저장됩니다. 복제된 데이터에 대한 수정 사항은 프로덕션 환경에 영향을 미치지 않아야 합니다. 이 데이터에 액세스하는 소프트웨어는 지속적으로 높은 I/O 성능을 요구합니다.
솔루션 아키텍트는 프로덕션 데이터를 테스트 환경으로 복제하는 데 필요한 시간을 최소화해야 합니다.
다음 중 어떤 솔루션이 이러한 요구 사항을 충족할까요?

A. 프로덕션 EBS 볼륨의 EBS 스냅샷을 생성합니다. 테스트 환경의 EC2 인스턴스 스토어 볼륨에 스냅샷을 복원합니다.
B. 프로덕션 EBS 볼륨을 EBS 멀티 어태치 기능을 사용하도록 구성합니다. 프로덕션 EBS 볼륨의 EBS 스냅샷을 생성합니다.
프로덕션 EBS 볼륨을 테스트 환경의 EC2 인스턴스에 연결합니다.
C. 프로덕션 EBS 볼륨의 EBS 스냅샷을 생성합니다. 새 EBS 볼륨을 생성하고 초기화합니다. 새 EBS 볼륨을 EC2 인스턴스에 연결합니다.
프로덕션 EBS 스냅샷에서 볼륨을 복원하기 전에 테스트 환경에서 이 작업을 수행합니다.
D. 프로덕션 EBS 볼륨의 EBS 스냅샷을 생성합니다. EBS 스냅샷에서 빠른 스냅샷 복원 기능을 활성화합니다. 스냅샷을 새 EBS 볼륨으로 복원합니다. 새 EBS 볼륨을 테스트 환경의 EC2 인스턴스에 연결합니다.

EBS 스냅샷 복원 특징 : 
일반 스냅샷에서 복원한 EBS 볼륨은
처음 접근할 때 S3에서 데이터 가져옴
-> Lazy loading
-> 초기 I/O 성능 저하 발생

해결 방법
EBS FSR
스냅샷에서 복원한 볼륨이
    즉시 프로비저닝된 성능
    첫 접근 지연 X
최소 시간 + 고성능 문제에서 정답

정답 : D
## Q11(pdf Q#21)
한 전자상거래 회사가 AWS에서 매일 한 가지 상품만 할인 판매하는 웹사이트를 구축하려고 합니다.
이 회사는 피크 시간대에 밀리초 단위의 지연 시간으로 시간당 수백만 건의 요청을 처리할 수 있어야 합니다.
다음 중 운영 오버헤드가 가장 적은 솔루션은 무엇일까요?

A. Amazon S3를 사용하여 웹사이트 전체를 여러 S3 버킷에 호스팅합니다. Amazon CloudFront 배포를 추가합니다. S3 버킷을 배포의 오리진으로 설정합니다.
주문 데이터를 Amazon S3에 저장합니다.
B. 여러 가용 영역에 걸쳐 Auto Scaling 그룹으로 실행되는 Amazon EC2 인스턴스에 웹사이트 전체를 배포합니다. 웹사이트 트래픽 분산을 위해 애플리케이션 로드 밸런서(ALB)를 추가합니다.
C. 백엔드 API용 ALB를 하나 더 추가합니다. 데이터를 Amazon RDS for MySQL에 저장합니다.
C. 전체 애플리케이션을 컨테이너에서 실행되도록 마이그레이션합니다. 컨테이너를 Amazon Elastic Kubernetes Service(Amazon EKS)에 호스팅합니다. Kubernetes 클러스터 오토스케일러를 사용하여 트래픽 급증 시 처리량을 조절하기 위해 Pod 수를 늘리거나 줄입니다.
데이터는 Amazon RDS for MySQL에 저장합니다.
D. Amazon S3 버킷을 사용하여 웹사이트의 정적 콘텐츠를 호스팅합니다. Amazon CloudFront 배포를 실행하고 S3 버킷을 오리진으로 설정합니다.
백엔드 API에는 Amazon API Gateway와 AWS Lambda 함수를 사용합니다. 데이터는 Amazon DynamoDB에 저장합니다.

D. S3 + CloudFront + API Gateway + Lambda + DynamoDB
정적 컨텐츠
    S3 + cloudfront
    전세계 캐싱
    밀리초 응답 가능
백엔드 api
    api gateway + lambda
    요청수에 따라 자동 확장
    서버 관리 불필요
데이터 저장
    dynamoDB
    대규모 트래픽처리
    밀리초 지연
    완전 관리형

## Q12(pdf Q#23)
한 회사가 Amazon S3 Standard 스토리지를 사용하여 백업 파일을 저장하고 있습니다. 이 파일은 1개월 동안 자주 액세스되지만, 1개월 후에는 액세스되지 않습니다. 회사는 파일을 무기한으로 보관해야 합니다.
이러한 요구 사항을 가장 비용 효율적으로 충족하는 스토리지 솔루션은 무엇입니까?

A. S3 Intelligent-Tiering을 구성하여 객체를 자동으로 마이그레이션합니다.
B. 1개월 후 S3 Standard에서 S3 Glacier Deep Archive로 객체를 전환하는 S3 Lifecycle 구성을 생성합니다.
C. 1개월 후 S3 Standard에서 S3 Standard-IA(S3 Standard-Infrequent Access)로 객체를 전환하는 S3 Lifecycle 구성을 생성합니다.
D. 1개월 후 S3 Standard에서 S3 One Zone-IA(S3 One Zone-Infrequent Access)로 객체를 전환하는 S3 Lifecycle 구성을 생성합니다.

정답 : B

## Q13(pdf Q#33)
한 회사가 AWS에서 온라인 마켓플레이스 웹 애플리케이션을 운영하고 있습니다. 이 애플리케이션은 피크 시간대에 수십만 명의 사용자를 처리합니다.
이 회사는 수백만 건의 금융 거래 내역을 여러 내부 애플리케이션과 공유하기 위한 확장 가능하고 거의 실시간에 가까운 솔루션이 필요합니다.
또한 거래 내역은 민감한 데이터를 제거한 후, 지연 시간이 짧은 문서 데이터베이스에 저장하여 빠르게 검색할 수 있도록 처리되어야 합니다.
이러한 요구 사항을 충족하기 위해 솔루션 아키텍트는 어떤 솔루션을 추천해야 할까요?

A. Store the transactions data into Amazon DynamoDB. Set up a rule in DynamoDB to remove sensitive data from every transaction upon
write. Use DynamoDB Streams to share the transactions data with other applications.
B. Stream the transactions data into Amazon Kinesis Data Firehose to store data in Amazon DynamoDB and Amazon S3. Use AWS Lambda
integration with Kinesis Data Firehose to remove sensitive data. Other applications can consume the data stored in Amazon S3.
C. Stream the transactions data into Amazon Kinesis Data Streams. Use AWS Lambda integration to remove sensitive data from every
transaction and then store the transactions data in Amazon DynamoDB. Other applications can consume the transactions data off the Kinesis
data stream.
D. Store the batched transactions data in Amazon S3 as les. Use AWS Lambda to process every le and remove sensitive data before
updating the les in Amazon S3. The Lambda function then stores the data in Amazon DynamoDB. Other applications can consume
transaction les stored in Amazon S3.

Kinesis Data Streams
    초고속, 실시간 데이터 스트리밍
    여러 소비자 애플리케이션이 동시에 읽기 가능
    대규모 트랜잭션 처리에 최적
AWS Lambda
    스트림에서 데이터 읽어서
    민감 정보 제거 (마스킹/필터링)
DynamoDB
    문서 데이터 저장
    밀리초 단위 지연
    자동 확장

정답 : C
## Q14(pdf Q#36)
한 회사가 AWS 클라우드에서 애플리케이션을 개발하고 있습니다. 이 애플리케이션은 두 개의 AWS 리전에 있는 Amazon S3 버킷에 데이터를 저장합니다. 이 회사는
AWS KMS(AWS Key Management Service) 고객 관리형 키를 사용하여 S3 버킷에 저장된 모든 데이터를 암호화해야 합니다.
두 S3 버킷의 데이터는 모두 동일한 KMS 키로 암호화 및 복호화되어야 합니다. 데이터와 키는 각각 두 리전에 저장되어야 합니다.
이러한 요구 사항을 가장 적은 운영 오버헤드로 충족하는 솔루션은 무엇일까요?

A. 각 리전에 S3 버킷을 생성합니다. Amazon S3 관리형 암호화 키(SSE-S3)를 사용하여 서버 측 암호화를 사용하도록 S3 버킷을 구성합니다.
S3 버킷 간 복제를 구성합니다.
B. 고객 관리형 다중 리전 KMS 키를 생성합니다. 각 리전에 S3 버킷을 생성합니다. S3 버킷 간 복제를 구성합니다.
애플리케이션이 클라이언트 측 암호화를 사용하여 KMS 키를 사용하도록 구성합니다.
C. 각 리전에 고객 관리형 KMS 키와 S3 버킷을 생성합니다. Amazon S3 관리형 암호화 키(SSE-S3)를 사용하여 서버 측 암호화를 사용하도록 S3 버킷을 구성합니다.
S3 버킷 간 복제를 구성합니다.
D. 각 리전에 고객 관리형 KMS 키와 S3 버킷을 생성합니다. AWS KMS 키(SSE-KMS)를 사용하여 서버 측 암호화를 사용하도록 S3 버킷을 구성합니다.
S3 버킷 간 복제를 구성합니다.

AWS KMS Multi-Region Key

동일한 키 머티리얼을 가진 키를 여러 리전에 생성
리전별로 존재하지만 논리적으로 같은 키
교차 리전 암·복호화 가능
이 요구사항을 만족하는 유일한 KMS 기능

Multi-Region KMS key
    동일 키 머티리얼
    각 리전에 키 존재
S3 버킷도 리전별로 생성
복제 구성 가능

정답 : B

## Q15(pdf Q#38)
한 회사가 Amazon S3에 정적 웹사이트를 호스팅하고 Amazon Route 53을 DNS로 사용하고 있습니다. 이 웹사이트는 전 세계에서 접속량이 증가하고 있습니다. 회사는 웹사이트에 접속하는 사용자의 지연 시간을 줄여야 합니다.
다음 중 이러한 요구 사항을 가장 비용 효율적으로 충족하는 솔루션은 무엇입니까?

A. 웹사이트가 포함된 S3 버킷을 모든 AWS 리전에 복제합니다. Route 53 지리적 위치 라우팅 항목을 추가합니다.
B. AWS 글로벌 가속기에서 가속기를 프로비저닝합니다. 제공된 IP 주소를 S3 버킷과 연결합니다. Route 53 항목을 수정하여
가속기의 IP 주소를 가리키도록 합니다.
C. S3 버킷 앞에 Amazon CloudFront 배포를 추가합니다. Route 53 항목을 수정하여 CloudFront 배포를 가리키도록 합니다.
D. 버킷에서 S3 전송 가속을 활성화합니다. Route 53 항목을 수정하여 새 엔드포인트를 가리키도록 합니다.

정답 : C
