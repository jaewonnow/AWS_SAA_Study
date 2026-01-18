# Week03 - S3, Ebs, EFs

## Q14

### 🧩 문제 요약

온프레미스 애플리케이션을 AWS로 이전하려고 하며 출력 파일 크기가 수십 GB부터 수백 TB까지 다양하고 표준 파일시스템 디렉터리 구조로 저장되어야 한다. 자동 확장, 고가용성, 최소 운영 오버헤드를 만족해야 한다.

### ✅ 정답

**C. Migrate the application to Amazon EC2 instances in a Multi-AZ Auto Scaling group. Use Amazon Elastic File System (Amazon EFS) for storage.**

### 🔍 정리

- EFS는 관리형 NFS 파일 시스템으로 파일/폴더 구조를 그대로 제공하고 수백 TB까지 자동 확장 가능

- Multi-AZ로 고가용성을 제공하며 여러 EC2 인스턴스에서 동시에 마운트할 수 있음

- EBS는 인스턴스에 붙는 블록 스토리지라 공유/확장/운영 측면에서 요구사항에 부적합

## Q221

### 🧩 문제 요약

Amazon Linux EC2 여러 대에서 생성되는 애플리케이션 로그를 7년간 보관해야 하고 리포팅 도구가 모든 로그 파일에 동시에 접근해 분석할 수 있어야 하며 비용은 최대한 절감해야 한다.

### ✅ 정답

**D. Amazon S3**

### 🔍 정리

- S3는 대규모 로그를 저비용·고내구성으로 장기 보관하기에 가장 적합하고, 다수 클라이언트의 동시 접근도 문제 없음

- 7년 보관은 S3 Lifecycle(Glacier/Deep Archive) 로 더 저렴하게 최적화 가능

- EBS/Instance Store는 서버 종속적이고 내구성/확장/비용 측면에서 장기 보관에 부적합, EFS는 파일 공유엔 좋지만 로그 장기보관 비용이 더 큼

## Q252

중요한 고객 케이스 파일을 저장해야 하고 파일 수는 계속 증가하며 여러 EC2 애플리케이션 서버에서 동시에 접근 가능해야 하고 내장된 이중화(중복성)가 필요하다.

### ✅ 정답

**A. Amazon Elastic File System (Amazon EFS)**

### 🔍 정리

- EFS는 관리형 파일 시스템(NFS)으로 여러 EC2에서 동시에 마운트/접근 가능

- 자동 확장 + 내장된 고가용성/이중화(멀티 AZ) 제공

- EBS는 기본적으로 단일 인스턴스용 블록 스토리지라 “동시 접근/공유” 요구에 부적합

`여러 EC2에서 동시에 ‘파일 시스템처럼’ 쓰는 경우”는 S3가 아니라 EFS`

## Q3

AWS Organizations를 사용해 여러 계정을 관리하고 있으며 관리 계정의 S3 버킷에 있는 프로젝트 보고서에 대해 조직(Organization) 내부 계정의 사용자만 접근하도록 제한하고 싶고 운영 오버헤드를 최소화해야 한다.

### ✅ 정답

**A. Add the aws:PrincipalOrgID global condition key with a reference to the organization ID to the S3 bucket policy.**

### 🔍 정리

- aws:PrincipalOrgID 조건 키를 사용하면 현재 조직에 속한 모든 계정의 사용자만 자동으로 허용/차단 가능

- 계정 추가/제거 시 정책을 수정할 필요가 없어 운영 오버헤드가 최소

- OU 경로(aws:PrincipalOrgPaths)는 구조 변경 시 정책 수정이 필요할 수 있음

- CloudTrail 기반 수동 갱신이나 태그 기반 제어는 관리 부담이 큼

## Q5

두 AZ에 EC2+EBS를 각각 두고 ALB 뒤에 붙였더니 사용자가 새로고침할 때마다 서로 다른 서버로 분산되면서 각 서버에 저장된 문서 “일부만” 보여 전체 문서를 한 번에 볼 수 없는 상태다.

### ✅ 정답

**C. Copy the data from both EBS volumes to Amazon EFS. Modify the application to save new documents to Amazon EFS**

### 🔍 정리

- EBS는 인스턴스/AZ 단위 블록 스토리지라 서버마다 데이터가 분리되어 문서가 갈라져 보이는 현상이 발생함

- 여러 EC2가 동시에 같은 파일을 봐야 하면 공유 파일 시스템(EFS) 로 중앙화해야 함 (Multi-AZ, 동시 마운트)

- ALB로 특정 서버에 고정(B)은 근본 해결이 아니고 데이터 복제(A)는 운영 부담/동기화 문제 큼

## Q6

### 🧩 문제 요약

온프레미스 NAS(NFS)에 있는 총 70TB의 대용량 비디오 파일(최대 500GB)을 S3로 옮겨야 하며 가능한 한 빨리 마이그레이션하되 네트워크 대역폭 사용을 최소화해야 한다.

### ✅ 정답

**B. Create an AWS Snowball Edge job. Receive a Snowball Edge device on premises. Use the Snowball Edge client to transfer data to the device. Return the device so that AWS can import the data into Amazon S3.**

### 🔍 정리

- 대용량(수십 TB+) 빠른 이전 + 네트워크 최소 사용 조합이면 Snowball이 정석(오프라인 물리 전송)

- AWS CLI(A)나 File Gateway(C/D)는 결국 네트워크로 70TB를 보내야 해서 “대역폭 최소” 조건에 불리

- Direct Connect(D)도 네트워크 전송 자체는 필요하므로 “최소 대역폭” 관점에서는 Snowball이 가장 적합

## Q33

### 🧩 문제 요약

피크 시간에 대규모 사용자를 처리하는 마켓플레이스에서 수백만 건의 금융 거래 데이터를 여러 내부 애플리케이션과 확장 가능하고 거의 실시간으로 공유해야 하고 저장 전에 민감정보를 제거한 뒤 문서 DB에 저장해 저지연 조회가 가능해야 한다.

### ✅ 정답

**C. Stream the transactions data into Amazon Kinesis Data Streams. Use AWS Lambda integration to remove sensitive data from every transaction and then store the transactions data in Amazon DynamoDB. Other applications can consume the transactions data off the Kinesis data stream.**

### 🔍 정리

- Kinesis Data Streams는 여러 컨슈머가 동시에 읽을 수 있는 확장형 실시간 스트리밍(팬아웃) 구조에 적합

- Lambda로 실시간 변환(민감정보 마스킹/제거) 후 저장하는 패턴이 표준

- Firehose는 주로 배달/적재(목적지로 전송)에 강하고 여러 앱이 스트림에서 직접 near-real-time로 소비하는 요구에는 KDS가 더 적합

## Q36

### 🧩 문제 요약

두 리전에 있는 S3 버킷에 저장되는 모든 데이터를 KMS 고객 관리형 키로 암호화해야 하고 두 버킷의 데이터가 같은 KMS 키로 암·복호화되어야 한다. 데이터와 키가 두 리전에 모두 존재해야 하고 운영 오버헤드는 최소여야 한다.

### ✅ 정답

**B. Create a customer managed multi-Region KMS key. Create an S3 bucket in each Region. Configure replication between the S3 buckets. Configure the application to use the KMS key with client-side encryption.**

### 🔍 정리

- Multi-Region KMS key는 “같은 키(논리적으로 동일)”를 두 리전에 복제된 형태로 유지할 수 있어 “키도 두 리전에 존재” 요구를 만족

## Q38

S3 정적 웹사이트가 전 세계에서 접속 증가로 지연이 커져서 전 세계 사용자 지연 시간을 가장 비용 효율적으로 줄여야 한다.

### ✅ 정답

**C. Add an Amazon CloudFront distribution in front of the S3 bucket. Edit the Route 53 entries to point to the CloudFront distribution.**

### 🔍 정리

- 정적 콘텐츠의 글로벌 지연 개선은 CloudFront(CDN) 가 정석이며 엣지 캐싱으로 지연을 크게 줄임

- S3 버킷을 전 리전에 복제(A)는 운영/비용 부담이 큼

- Global Accelerator(B)는 주로 TCP/UDP 애플리케이션 가속용이며 S3 정적 사이트에 비효율적

## Q59

### 🧩 문제 요약

공개된 서버리스 애플리케이션(API Gateway + Lambda)에 대해 봇넷으로 인한 비정상 트래픽이 급증했고 권한 없는 요청을 차단해야 한다. (2가지)

### ✅ 정답

**A. Create a usage plan with an API key that is shared with genuine users only.**

**C. Implement an AWS WAF rule to target malicious requests and trigger actions to filter them out.**

### 🔍 정리

- API Gateway Usage Plan + API Key로 합법 사용자만 접근하도록 제한하고 쿼터/스로틀링으로 남용을 억제

- AWS WAF를 API Gateway 앞단에 적용해 봇/악성 패턴을 사전에 필터링(IP, rate-based, managed rules)

## Q64

### 🧩 문제 요약

사용자가 업로드한 문서를 저장한 뒤 규제 요구사항에 따라 수정이나 삭제가 불가능해야 하며 웹/모바일 앱에서 업로드되는 프로덕션 환경의 문서에 적용해야 한다.

### ✅ 정답

**A. Store the uploaded documents in an Amazon S3 bucket with S3 Versioning and S3 Object Lock enabled.**

### 🔍 정리

- S3 Object Lock (WORM) 은 객체를 수정·삭제 불가 상태로 강제하여 규제/컴플라이언스 요구 충족

- S3 Versioning 은 Object Lock 사용의 필수 전제이며 버전 단위로 보호 가능

## Q118

### 🧩 문제 요약

여러 AZ의 EC2에서 동작하는 웹앱이 약 900TB 규모의 텍스트 문서 저장소를 제공해야 하고 수요가 급증하는 구간에도 항상 확장 가능해야 하며 전체 비용을 최대한 낮춰야 한다.

### ✅ 정답

**D. Amazon S3**

### 🔍 정리

- 900TB 같은 초대용량 데이터는 S3 객체 스토리지가 가장 비용 효율적이고 거의 무제한 자동 확장을 제공

- 다수 EC2/사용자가 동시에 접근하는 읽기 트래픽에도 S3는 확장성이 높아 수요 급증에 유리

- EBS/EFS는 파일시스템/블록스토리지라 대용량·대규모 분산 접근에서 비용이 크게 증가할 가능성이 큼

## Q127

### 🧩 문제 요약

비디오 처리용으로 최고 I/O 성능의 10TB 스토리지가 필요하고 미디어 콘텐츠 보관용으로 매우 내구성이 높은 300TB가 필요하다. 사용하지 않는 아카이브 미디어를 위해 900TB의 장기 보관 스토리지가 필요하다.

### ✅ 정답

**A. Amazon EBS for maximum performance, Amazon S3 for durable data storage, and Amazon S3 Glacier for archival storage**

### 🔍 정리

- 고성능 블록 스토리지는 EBS(io1/io2 계열) 가 대표적 선택지

- 대용량 내구성 스토리지는 S3(객체 스토리지, 높은 내구성) 가 정석

- 장기 미사용 아카이브는 S3 Glacier가 가장 비용 효율적

## Q384

오토스케일링으로 늘었다 줄었다 하는 무상태(stateless) EC2 웹 3티어와 RDS PostgreSQL로 구성된 환경에서 RPO 2시간을 만족하면서 확장성·자원 효율을 최대화하는 백업 전략이 필요하다. (EC2는 로컬 임시 스토리지 필요 없음)

### ✅ 정답

**C. Retain the latest Amazon Machine Images (AMIs) of the web and application tiers. Enable automated backups in Amazon RDS and use point-in-time recovery to meet the RPO.**

### 🔍 정리

- Stateless + ASG 환경은 인스턴스(EBS) 단위 백업보다 재배포 가능한 이미지(AMI) 기반 복구가 더 확장성/효율이 좋음

- RDS 자동 백업 + PITR(Point-in-time recovery) 로 원하는 시점(최대 2시간 이내)까지 복구 가능해 RPO 충족

- EC2를 2시간마다 EBS 스냅샷(A/B/D) 뜨는 방식은 인스턴스가 계속 바뀌는 ASG에서 불필요한 백업이 많아지고 자원 활용이 비효율적

## Q648

### 🧩 문제 요약

데이터센터의 HPC 환경을 AWS로 확장하려고 하며 수백 GB 데이터를 지속적으로 높은 처리량으로 서브 밀리초 지연에 가깝게 처리해야 한다. 저장소는 고가용성이어야 하고 수천 대의 컴퓨팅 인스턴스가 동시에 전체 데이터셋에 접근해 처리할 수 있어야 한다.

### ✅ 정답

**B. Use Amazon FSx for Lustre persistent file systems.**

### 🔍 정리

- HPC + 초저지연/고처리량 + 대규모 동시 접근 패턴은 Lustre가 정답 영역(병렬 파일 시스템)

- FSx for Lustre는 수천 노드가 동시에 읽고 쓰는 워크로드에 최적화되어 지속 처리량(sustained throughput) 에 강함

- Scratch는 일시적(내구성/복구 요구에 약함)인 워크로드에 더 적합하고 문제는 “고가용성 저장소”를 요구하므로 persistent가 더 맞음

- EFS는 범용 NFS로 좋지만 이 문제 수준의 HPC 성능/지연 요구에는 FSx for Lustre가 더 적합
