# Week07 - Route 53 , S3 , CloudFront

## Q12

### 🧩 문제 요약

전 세계 사용자가 접속하는 웹앱이 EC2 + ALB 뒤에 있고 정적 데이터는 S3에 있다. 정적/동적 모두 지연을 줄이고 성능을 개선해야 하며 도메인은 Route 53을 사용 중이다.

### ✅ 정답

**A. Create an Amazon CloudFront distribution that has the S3 bucket and the ALB as origins. Configure Route 53 to route traffic to the CloudFront distribution.**

### 🔍 정리

- 정적 콘텐츠는 CloudFront + S3 오리진 → 엣지 캐싱으로 전 세계 지연 최소화

- 동적 콘텐츠는 CloudFront + ALB 오리진 → 엣지에서 ALB로 최적 경로(필요 시 캐시/가속)로 전달해 지연 개선

- Route 53은 CloudFront 배포로 라우팅 → 단일 도메인으로 정적/동적 모두 처리 가능, 구성 단순

## Q29

### 🧩 문제 요약

UDP 기반 VoIP 서비스가 멀티 리전에 배포되어 있고 사용자를 최저 지연 리전으로 라우팅해야 한다. 또한 리전 간 자동 장애조치가 필요하다.

### ✅ 정답

**A. Deploy a Network Load Balancer (NLB) and an associated target group. Associate the target group with the Auto Scaling group. Use the NLB as an AWS Global Accelerator endpoint in each Region.**

### 🔍 정리

- 프로토콜이 UDP → **NLB(L4)**가 적합(UDP 지원), ALB는 UDP 미지원이라 불가

- 글로벌 라우팅은 AWS Global Accelerator → Anycast로 사용자에게 가장 가까운 엣지로 유입시킨 뒤 가장 낮은 지연의 정상(healthy) 리전 엔드포인트로 라우팅

- 장애조치는 Global Accelerator 헬스체크 기반 자동 failover → 리전 장애 시 다른 리전 NLB로 빠르게 전환

## Q38

### 🧩 문제 요약

S3 정적 웹사이트 + Route 53 DNS를 사용 중이며 전 세계 트래픽 증가로 글로벌 사용자 지연을 줄여야 한다. 목표는 가장 비용 효율적인 방식이다.

### ✅ 정답

**C. Add an Amazon CloudFront distribution in front of the S3 bucket. Edit the Route 53 entries to point to the CloudFront distribution.**

### 🔍 정리

- 정적 콘텐츠는 CloudFront 엣지 캐싱 → 전 세계 PoP에서 가까운 위치로 제공해 지연 최소화

- S3 원본을 그대로 두고 Route 53을 CloudFront로만 변경 → 아키텍처 변경 최소 + 운영 부담 낮음

## Q56

### 🧩 문제 요약

Route 53에 등록한 회사 도메인으로 **API Gateway(리전: ca-central-1) URL을 커스텀 도메인 + HTTPS(인증서)**로 제공해 서드파티가 안전하게 호출하도록 해야 한다.

### ✅ 정답

**C. Create a Regional API Gateway endpoint. Associate the API Gateway endpoint with the company's domain name. Import the public certificate associated with the company's domain name into AWS Certificate Manager (ACM) in the same Region. Attach the certificate to the API Gateway endpoint. Configure Route 53 to route traffic to the API Gateway endpoint.**

### 🔍 정리

- API Gateway는 Regional Custom Domain 사용 → ca-central-1 리전에서 퍼블릭 엔드포인트를 회사 도메인으로 제공

- 인증서는 ACM 동일 리전(ca-central-1) 에서 발급/가져와 API Gateway 커스텀 도메인에 연결 → HTTPS 요구사항 충족

## Q120

### 🧩 문제 요약

자가 운영 DNS를 EC2 3대 + NLB로 us-west-2에 운영 중이고, eu-west-1에도 동일하게 EC2 3대 + NLB를 추가했다. 미국/유럽 사용자에 대해 **성능(최저 지연)**과 **가용성(리전 장애 시 자동 전환)**을 높이면서 **모든 EC2(두 리전의 두 NLB 뒤)**로 트래픽을 분산해야 한다.

### ✅ 정답

**B. Create a standard accelerator in AWS Global Accelerator. Create endpoint groups in us-west-2 and eu-west-1. Add the two NLBs as endpoints for the endpoint groups.**

### 🔍 정리

- 글로벌 라우팅은 AWS Global Accelerator → Anycast로 사용자에게 가장 가까운 엣지로 유입시켜 미국/유럽 최저 지연 리전으로 라우팅

## Q141

### 🧩 문제 요약

전 세계 사용자에게 HTTPS로 개인화된(정적+동적 혼합) 뉴스/알림/날씨 콘텐츠를 제공한다. 현재 EC2 API 서버 + ALB 구조이며 목표는 전 세계 사용자 지연을 최소화하는 설계다.

### ✅ 정답

**A. Deploy the application stack in a single AWS Region. Use Amazon CloudFront to serve all static and dynamic content by specifying the ALB as an origin.**

### 🔍 정리

- 글로벌 성능은 CloudFront가 핵심 → 전 세계 엣지에서 TLS 종료 및 콘텐츠 전송으로 사용자 체감 지연 최소

- 정적/동적 혼합이므로 ALB를 CloudFront 오리진으로 두면 동적 요청도 엣지를 통해 최적 경로로 전달되어 전송 지연을 줄일 수 있음

## Q217

### 🧩 문제 요약

글로벌 웹앱(EC2 + ALB)과 Amazon Aurora를 사용 중이다. DR이 필요하며 **최대 30분 다운타임(RTO)**과 **일부 데이터 손실(RPO)**은 허용된다. 평상시에는 DR 리전이 트래픽/부하를 처리할 필요가 없다.

### ✅ 정답

**A. Deploy the application with the required infrastructure elements in place. Use Amazon Route 53 to configure active-passive failover. Create an Aurora Replica in a second AWS Region..**

### 🔍 정리

- DB는 Cross-Region Aurora Replica → 비동기 복제로 일부 데이터 손실(RPO) 허용 조건에 부합하면서 DR 리전에서 빠르게 승격 가능

## Q224

### 🧩 문제 요약

단일 리전에 EC2로 리호스팅한 웹앱을 고가용성/장애 허용 구조로 재설계해야 한다. 또한 트래픽이 실행 중인 모든 EC2 인스턴스에 랜덤하게 도달해야 한다. (2개 선택)

### ✅ 정답

**C. Create an Amazon Route 53 multivalue answer routing policy.**
**E. Launch four EC2 instances: two instances in one Availability Zone and two instances in another Availability Zone.**

### 🔍 정리

- 라우팅은 Route 53 Multivalue Answer → 여러 IP를 반환하고(헬스체크 가능) 클라이언트가 반환된 값 중 하나로 연결하여 여러 EC2로 랜덤 분산 효과

- 인프라는 2개 AZ에 균등 분산(2+2) → AZ 장애 시에도 남은 AZ에서 최소 용량을 유지해 HA/FT 확보

## Q264

### 🧩 문제 요약

Route 53이 직접 EC2 인스턴스로 트래픽을 보내는 구조에서, 비정상( unhealthy ) 인스턴스의 IP가 DNS 응답에 포함되어 간헐적으로 타임아웃 오류가 발생하고 있다.

### ✅ 정답

**D. Create an Application Load Balancer (ALB) with a health check in front of the EC2 instances. Route to the ALB from Route 53.**

### 🔍 정리

- 트래픽 분산은 ALB가 담당 → 요청을 정상(Healthy) 인스턴스로만 라우팅하여 타임아웃 제거

- ALB의 내장 Health Check → 인스턴스 상태를 실시간으로 판단해 비정상 인스턴스 자동 제외

## Q265

### 🧩 문제 요약

웹/앱/DB 3계층을 고가용성으로 설계해야 한다. HTTPS 콘텐츠는 엣지에 최대한 가깝게(최소 지연) 제공해야 하며, 가장 보안적으로 안전한 구성이어야 한다.

### ✅ 정답

**C. Configure a public Application Load Balancer (ALB) with multiple redundant Amazon EC2 instances in private subnets. Configure Amazon CloudFront to deliver HTTPS content using the public ALB as the origin.**

### 🔍 정리

- 엣지 HTTPS 전송은 CloudFront → 전 세계 엣지에서 TLS 종료/캐싱/전송 최적화로 전달 시간 최소

- 오리진은 Public ALB → CloudFront가 단일 오리진으로 접근, 백엔드로의 진입점을 중앙화

- 웹/앱 EC2는 Private Subnet 배치 → 인스턴스를 인터넷에 직접 노출하지 않아 공격 표면 최소(가장 보안적)

## Q302

### 🧩 문제 요약

모바일 앱이 슬로모션 영상을 RAW로 S3에 업로드하고 그대로 S3에서 내려받아 재생한다. RAW가 너무 커서 버퍼링/재생 문제가 발생한다. 목표는 성능·확장성 최대화 + 운영 오버헤드 최소화다. (2개 선택)

### ✅ 정답

**A. Deploy Amazon CloudFront for content delivery and caching.**
**C. Use Amazon Elastic Transcoder to convert the video files to more appropriate formats.**

### 🔍 정리

- 전송 성능은 CloudFront → 글로벌 엣지 캐싱/전송 최적화로 모바일 사용자 지연·버퍼링 감소 + 대규모 트래픽에도 자동 확장

- 재생 최적화는 Elastic Transcoder → RAW를 스트리밍에 적합한 코덱/비트레이트/해상도로 변환해 파일 크기 감소 및 재생 안정화

## Q367

### 🧩 문제 요약

전 세계 사용자에게 UDP 기반 온프레미스 애플리케이션(미국/아시아/유럽 DC)에 Route 53 latency-based routing으로 라우팅 중이다. 애플리케이션은 반드시 온프레미스에 있어야 하며 성능과 가용성을 더 높이고 싶다.

### ✅ 정답

**A. Configure three Network Load Balancers (NLBs) in the three AWS Regions to address the on-premises endpoints. Create an accelerator by using AWS Global Accelerator, and register the NLBs as its endpoints. Provide access to the application by using a CNAME that points to the accelerator DNS.**

### 🔍 정리

- 글로벌 성능/가용성은 AWS Global Accelerator → Anycast로 사용자에게 가장 가까운 엣지로 유입 후 최저 지연 경로로 전달 + 헬스체크 기반 빠른 장애조치

- 프로토콜이 UDP → **NLB(L4)**만 적합(ALB는 UDP 미지원)

## Q408

### 🧩 문제 요약

전 세계에 분산된 수천 대 UDP 디바이스가 데이터를 보내고, 앱이 즉시 처리 후 응답한다(저장 없음). 목표는 최소 지연 + 리전 간 빠른 자동 장애조치다.

### ✅ 정답

**B. Use AWS Global Accelerator. Create a Network Load Balancer (NLB) in each of the two Regions as an endpoint. Create an Amazon Elastic Container Service (Amazon ECS) cluster with the Fargate launch type. Create an ECS service on the cluster. Set the ECS service as the target for the NLB. Process the data in Amazon ECS.**

### 🔍 정리

- 글로벌 라우팅/가속은 AWS Global Accelerator → Anycast로 가장 가까운 엣지로 유입, 헬스체크 기반으로 최저 지연 리전 선택 + 빠른 failover

- 프로토콜이 UDP → NLB(L4) 필요(UDP 지원), ALB는 UDP 미지원

## Q461

### 🧩 문제 요약

단일 리전에 EC2 ASG로 모바일 게임 서버를 운영 중이고, DynamoDB를 사용한다. 사용자↔서버 통신에 TCP + UDP가 모두 필요하며, 전 세계 사용자가 사용한다. 목표는 전 세계 최저 지연이다.

### ✅ 정답

**B. Use AWS Global Accelerator to create an accelerator. Create a Network Load Balancer (NLB) behind an accelerator endpoint that uses Global Accelerator integration and listening on the TCP and UDP ports. Update the Auto Scaling group to register instances on the NLB.**

### 🔍 정리

- 글로벌 최저 지연은 AWS Global Accelerator → Anycast로 사용자에게 가장 가까운 엣지로 유입 후 AWS 글로벌 백본으로 단일 리전까지 최적 경로 제공

## Q464

### 🧩 문제 요약

주문 데이터가 RDS for PostgreSQL Single-AZ에 저장되어 단일 장애 지점(SPOF)이 있다. 애플리케이션 코드 변경 없이 DB 다운타임을 최소화하고 가용성을 높여야 한다.

### ✅ 정답

**A. Convert the existing database instance to a Multi-AZ deployment by modifying the database instance and specifying the Multi-AZ option.**

### 🔍 정리

- DB는 RDS Multi-AZ로 전환 → 동기식 스탠바이 + 자동 장애조치로 SPOF 제거 및 다운타임 최소화

- 애플리케이션은 엔드포인트 그대로 사용 → 코드 변경 없이 Failover 처리 가능

## Q527

### 🧩 문제 요약

단일 리전에서 EC2 기반 웹/앱 서버(ASG + ELB)로 스트리밍 서비스를 운영 중이며, DB는 Aurora Global Database를 사용한다. 글로벌 확장과 함께 다운타임을 최소화하면서 **가장 높은 장애 허용(FT)**을 원한다.

### ✅ 정답

**D. Deploy the web tier and the application tier to a second Region. Use an Amazon Aurora global database to deploy the database in the primary Region and the second Region. Use Amazon Route 53 health checks with a failover routing policy to the second Region. Promote the secondary to primary as needed.**

### 🔍 정리

- 애플리케이션 계층은 2번째 리전에 동일 스택(웹/앱 + ASG/ELB) 배포 → 리전 장애에도 서비스 지속(리전 단위 FT)

- DB는 Aurora Global Database(Primary + Secondary Region) → 리전 간 저지연 복제로 DR/Failover에 최적, 필요 시 Secondary를 승격(promote)

## Q538

### 🧩 문제 요약

CloudFront를 사용하는 글로벌 영상 스트리밍 서비스가 국가별 단계적 롤아웃을 한다. 롤아웃 대상 국가 외의 사용자는 콘텐츠를 시청하지 못하게 해야 한다.

### ✅ 정답

**A. Add geographic restrictions to the content in CloudFront by using an allow list. Set up a custom error message.**

### 🔍 정리

- 접근 제어는 CloudFront Geographic Restrictions(Allow list) → 허용한 국가에서만 콘텐츠 제공, 그 외 국가는 차단

- 국가 기반 제어는 CloudFront 엣지에서 즉시 적용 → 추가 인증 로직/URL 관리 없이 운영 오버헤드 최소
