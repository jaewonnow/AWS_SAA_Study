# Week02 - Gateway, VPC

## Q3

### 🧩 문제 요약

VPC 내부의 EC2 인스턴스가 인터넷 연결 없이
Amazon S3 버킷에 접근해야 하는 상황이다.

### ✅ 정답

**A. Create a gateway VPC endpoint to the S3 bucket.**

### 🔍 정리

- S3는 **Gateway VPC Endpoint**
- EC2 ↔ S3를 **인터넷 없이 연결 가능**
- IAM Role ≠ 네트워크 해결

## Q19

### 🧩 문제 요약

퍼블릭 서브넷에 있는 웹 서버로 들어오는 모든 트래픽을 사전에 검사해야 한다.
AWS Marketplace에서 배포한 서드파티 가상 방화벽(appliance) 이 있고
이 방화벽은 IP 패킷 단위로 트래픽을 검사할 수 있다.
운영 오버헤드는 최소화해야 한다.

#### ✅ 정답

**D. Deploy a Gateway Load Balancer in the inspection VPC. Create a Gateway Load Balancer endpoint to receive the incoming packets and forward the packets to the appliance.**

### 🔍 정리

- 서드파티 방화벽처럼 L3/L4(IP 패킷) 기반 검사에는 Gateway Load Balancer(GWLB) 가 최적

- GWLB는 투명한 트래픽 인라인 검사를 지원

- Gateway Load Balancer Endpoint(GWLBe) 를 통해 다른 VPC 트래픽을 손쉽게 연결 가능

- 방화벽 확장/축소 및 관리가 자동화되어 운영 오버헤드 최소화

## Q101

### 🧩 문제 요약

IPv4 기반의 멀티 AZ VPC 환경에서 프라이빗 서브넷에 있는 EC2 인스턴스가 외부에서 접근되지 않으면서도 소프트웨어 업데이트를 위해 인터넷 접근이 가능해야 한다.

### ✅ 정답

**A. Create three NAT gateways, one for each public subnet in each AZ. Create a private route table for each AZ that forwards non-VPC traffic to the NAT gateway in its AZ.**

### 🔍 해설

- 프라이빗 서브넷에서 IPv4 인터넷 접근을 제공하려면 NAT Gateway가 필요

- AZ별 NAT Gateway 구성은 고가용성과 장애 격리를 보장

- NAT Instance는 수동 관리가 필요해 운영 부담이 큼

- Internet Gateway는 퍼블릭 서브넷 전용

- Egress-only Internet Gateway는 IPv6 환경에서만 사용

## Q125

### 🧩 문제 요약

이커머스 2티어 아키텍처에서 EC2와 RDS는 인터넷에 직접 노출되면 안 되지만 EC2는 외부 결제 서비스 호출을 위해 인터넷 아웃바운드 접근이 필요하며 전체 시스템은 고가용성을 만족해야 한다. (2개)

### ✅ 정답

**A. Use an Auto Scaling group to launch the EC2 instances in private subnets. Deploy an RDS Multi-AZ DB instance in private subnets.**

**E. Configure a VPC with two public subnets, two private subnets, and two NAT gateways across two Availability Zones. Deploy an Application Load Balancer in the public subnets.**

### 🔍 해설

- EC2/RDS 비공개 요구사항 : 애플리케이션 서버와 DB는 프라이빗 서브넷에 배치해야 함 → A 충족

- 고가용성 : EC2는 Auto Scaling + 멀티 AZ, RDS는 Multi-AZ → A 충족

- 외부 결제 연동(아웃바운드 인터넷) : 프라이빗 서브넷의 EC2가 인터넷으로 나가려면 NAT Gateway 필요 → E 충족

- 인바운드 트래픽 처리 : 외부 트래픽 수신은 퍼블릭 서브넷의 ALB가 담당 → E 충족

- 퍼블릭 서브넷에 EC2를 두는 선택지는 보안 요구사항 위반

- 프라이빗 서브넷에 ALB 배치는 일반적인 인터넷 수신 아키텍처에 부적합

## Q176

### 🧩 문제 요약

프라이빗 서브넷에서 실행 중인 EC2 애플리케이션이 DynamoDB에 접근해야 하며 트래픽이 AWS 네트워크 밖으로 나가지 않도록 가장 안전한 방법이 필요하다.

### ✅ 정답

**A. Use a VPC endpoint for DynamoDB.**

### 🔍 해설

- DynamoDB는 Gateway VPC Endpoint를 통해 프라이빗하게 접근 가능

- VPC 엔드포인트를 사용하면 트래픽이 인터넷/NAT/IGW를 거치지 않고 AWS 내부망에서 처리됨

## Q251

### 🧩 문제 요약

프라이빗 서브넷에 있는 EC2 인스턴스가 외부 벤더로부터 보안 업데이트를 다운로드해야 하지만 서브넷 자체는 인터넷에 직접 노출되면 안 된다.

### ✅ 정답

**B. Create a NAT gateway, and place it in a public subnet. Configure the private subnet route table to use the NAT gateway as the default route.**

### 🔍 해설

- 프라이빗 서브넷의 EC2가 아웃바운드 인터넷 접근만 필요할 때는 NAT Gateway가 가장 안전하고 표준적인 방식

- NAT Gateway는 퍼블릭 서브넷에 위치하고 프라이빗 서브넷은 이를 통해 인터넷으로 나감

- Internet Gateway를 프라이빗 서브넷의 기본 라우트로 설정하면 인바운드 노출 위험이 있어 부적절

## Q272

### 🧩 문제 요약

미국 서부 리전에 있는 ALB 뒤의 EC2 기반 동적 웹사이트가 전 세계 사용자에게 다국어로 빠르게 응답해야 하지만 멀티 리전으로 아키텍처를 구성하지 않는다.

### ✅ 정답

**B. Configure an Amazon CloudFront distribution with the ALB as the origin. Set the cache behavior settings to cache based on the Accept-Language request header.**

### 🔍 해설

- 전 세계 사용자 지연 시간 감소에는 CloudFront(CDN) 가 가장 효과적

- 기존 아키텍처를 유지하면서 성능 개선 → ALB를 오리진으로 CloudFront 연결

- 다국어 지원은 Accept-Language 헤더 기준 캐시 분기로 해결

- S3로 교체(A)는 기존 동적 아키텍처를 재구성해야 하므로 조건 불충족

## Q294

### 🧩 문제 요약

EC2 인스턴스에서 S3 버킷에 접근해야 하며 트래픽이 인터넷을 거치지 않도록 구성해야 한다.

### ✅ 정답

**B. Set up a gateway VPC endpoint for Amazon S3 in the VPC.**

## Q324 (도전)

### 🧩 문제 요약

온프레미스에서 iSCSI로 마운트된 대용량 파일 스토리지를 사용 중이며 재해 복구를 구현하되 기존 인프라 변경을 최소화하고 엔드유저가 지연 없이 즉시 접근할 수 있어야 한다.

### ✅ 정답

**D. Provision an AWS Storage Gateway Volume Gateway stored volume with the same amount of disk space as the existing file storage volume. Mount the Volume Gateway stored volume to the existing file server by using iSCSI, and copy all files to the storage volume. Configure scheduled snapshots of the storage volume. To recover from a disaster, restore a snapshot to an Amazon Elastic Block Store (Amazon EBS) volume and attach the EBS volume to an Amazon EC2 instance.**

### 🔍 해설

- Volume Gateway (Stored Volume) 는 전체 데이터를 온프레미스에 로컬 저장하여 지연 없이 즉시 접근 가능

- 기존 iSCSI 스토리지를 그대로 쓰면서 스냅샷으로 백업해 두고 재해 시 EC2 + EBS로 빠르게 복구하는 구조
- 기존과 동일한 iSCSI 방식을 사용하므로 애플리케이션 변경이 거의 없음 → 변경 최소화

- AWS에는 스냅샷 형태로 비동기 백업되어 재해 복구 가능

- Cached Volume은 캐시에 없는 데이터 접근 시 지연 발생

- S3 File Gateway는 NFS/SMB로 접근 방식 변경 필요

- Tape Gateway는 장기 백업용으로 즉시 접근 요구사항에 부적합

## Q374

### 🧩 문제 요약

동일 리전 내 3개의 VPC 간 통신이 필요하고 단일 온프레미스 데이터센터로 매일 수백 GB의 대용량 데이터를 지연에 민감하게 전송해야 한다. 전체 구성은 비용 효율성을 최대화해야 한다.

### ✅ 정답

**D. Set up one AWS Direct Connect connection from the data center to AWS. Create a transit gateway, and attach each VPC to the transit gateway. Establish connectivity between the Direct Connect connection and the transit gateway.**

### 🔍 해설

- Direct Connect는 대용량·지연 민감 트래픽에 가장 적합한 전용 회선

- Transit Gateway를 사용하면 여러 VPC를 허브-스포크 구조로 단순하게 연결 가능

- 단일 Direct Connect + TGW 공유는 회선 수를 줄여 비용 절감

- VPC 간 통신(VPC-to-VPC)도 TGW를 통해 자연스럽게 해결

## Q439

### 🧩 문제 요약

IP 주소 범위가 작은 VPC에서 EC2 인스턴스 수가 증가하여 향후 워크로드에 사용할 IPv4 주소가 부족해졌고 이를 운영 오버헤드를 최소화하면서 해결해야 한다.

### ✅ 정답

**A. Add an additional IPv4 CIDR block to increase the number of IP addresses and create additional subnets in the VPC. Create new resources in the new subnets by using the new CIDR.**

### 🔍 해설

- VPC에는 추가 IPv4 CIDR 블록을 연결(secondary CIDR) 할 수 있어 IP 주소를 확장 가능

- 기존 VPC, 보안그룹, 라우팅 구조를 그대로 유지하면서 가장 단순하고 관리 부담이 적음

- 주소 부족 문제 해결에는 VPC 확장(secondary CIDR) 이 정석

## Q448

### 🧩 문제 요약

Management VPC는 단일 온프레미스 장비를 통한 VPN 연결만 사용하고 있어 단일 장애 지점(SPOF)이 존재하며 전체 아키텍처의 가용성을 높여야 한다.

### ✅ 정답

**C. Add a second set of VPNs to the Management VPC from a second customer gateway device.**

### 🔍 해설

- Management VPC는 단일 고객 게이트웨이(Customer Gateway) 에 의존하고 있어 장애 시 전체 연결이 끊김

- 두 번째 고객 게이트웨이 장비를 추가하고 이중 VPN 터널을 구성하면 SPOF 제거 가능

- VPC 간 VPN(A)이나 VGW 추가(B)는 근본 원인(단일 온프레미스 장비)을 해결하지 못함

## Q10

### 🧩 문제 요약

이커머스 애플리케이션에서 주문이 API Gateway로 들어오며 주문이 들어온 순서대로 처리되어야 한다.

### ✅ 정답

**B. Use an API Gateway integration to send a message to an Amazon Simple Queue Service (Amazon SQS) FIFO queue when the application receives an order. Configure the SQS FIFO queue to invoke an AWS Lambda function for processing.**

### 🔍 해설

- 순서 보장(ordered processing) 이 핵심 요구사항

- Amazon SQS FIFO queue는 메시지 순서 보장 + 정확히 한 번 처리를 제공

- API Gateway → SQS FIFO → Lambda 구조는 비동기 처리와 확장성도 충족

## Q42

### 🧩 문제 요약

여러 AZ에 분산된 프라이빗 서브넷의 EC2 인스턴스들이 S3에서 이미지를 다운로드/업로드하고 있으며 단일 NAT Gateway를 통해 통신하면서 리전 내 데이터 전송 비용이 발생해 이를 가장 비용 효율적으로 줄이고자 한다.

### ✅ 정답

**C. Deploy a gateway VPC endpoint for Amazon S3.**

### 🔍 해설

- S3 Gateway VPC Endpoint를 사용하면 EC2 ↔ S3 트래픽이 NAT Gateway를 거치지 않고 AWS 백본 네트워크로 직접 전달됨

- NAT Gateway 사용 시 AZ 간 트래픽이 발생하면 Regional data transfer charges가 부과됨

- VPC Endpoint는 데이터 전송 비용 절감 + 보안 강화를 동시에 달성

## Q92

### 🧩 문제 요약

민감한 사용자 정보를 저장한 S3 버킷에 대해 VPC 내부의 EC2 애플리케이션 티어에서만 안전하게 접근하도록 구성해야 한다. (2개)

### ✅ 정답

**A. Configure a VPC gateway endpoint for Amazon S3 within the VPC.**
**C. Create a bucket policy that limits access to only the application tier running in the VPC.**

### 🔍 해설

- VPC Gateway Endpoint for S3를 사용하면 EC2 ↔ S3 트래픽이 인터넷을 거치지 않고 AWS 내부 네트워크로 전달되어 보안성이 높아짐

- Bucket Policy로 특정 VPC(또는 VPC Endpoint)에서 오는 요청만 허용하면 접근 범위를 애플리케이션 티어로 제한 가능

## Q200

### 🧩 문제 요약

Amazon Cognito로 사용자 관리를 하고 있고 API Gateway에 호스팅된 REST API에 대해 AWS 관리형 방식으로 접근 제어를 수행해 개발 및 운영 오버헤드를 최소화하려고 한다.

### ✅ 정답

**D. Configure an Amazon Cognito user pool authorizer in API Gateway to allow Amazon Cognito to validate each request.**

### 🔍 해설

- Cognito User Pool Authorizer는 API Gateway와 완전 관리형으로 통합되어 토큰 검증을 자동 처리

- 별도의 Lambda 작성·유지보수가 필요 없어 운영 오버헤드 최소

## Q208

### 🧩 문제 요약

EC2 인스턴스에서 S3 버킷으로 데이터를 업로드해야 하고 API 호출과 데이터 트래픽이 퍼블릭 인터넷을 절대 통과하지 않아야 한다. 해당 EC2 인스턴스만 S3에 접근할 수 있어야 한다.

### ✅ 정답

**A. Create an interface VPC endpoint for Amazon S3 in the subnet where the EC2 instance is located. Attach a resource policy to the S3 bucket to only allow the EC2 instance’s IAM role for access.**

## Q296

### 🧩 문제 요약

기존 VPC(192.168.0.0/24)와 VPC 피어링을 하고 피어링이 가능한 가장 작은 CIDR 블록을 새 VPC에 할당해야 한다.

### ✅ 정답

**D. 10.0.1.0/24**

### 🔍 해설

- VPC 피어링을 하려면 CIDR 블록이 서로 겹치면 안 됨

- IPv4 VPC CIDR은 /16 ~ /28 범위만 허용됨

- /32는 VPC CIDR로 사용 불가 → A, C 탈락

- 192.168.0.0/24는 기존 VPC와 완전히 동일 → B 탈락

## Q471

### 🧩 문제 요약

VPC에서 컨테이너 기반 애플리케이션이 매일 대용량(1TB)의 데이터를 S3에 저장·조회한다. 비용을 최소화하고 인터넷을 경유하지 않도록 해야 한다.

### ✅ 정답

**C. Create a gateway VPC endpoint for Amazon S3. Associate this endpoint with all route tables in the VPC**

## Q684

### 🧩 문제 요약

온프레미스에서 AWS로 웹 애플리케이션을 이전하려고 한다. eu-central-1 리전과 지리적으로 가깝지만 규제로 인해 일부 애플리케이션은 해당 리전에 배포할 수 없고 단일 자릿수(ms) 지연 시간을 달성해야 한다.

### ✅ 정답

**B. Deploy the applications in AWS Local Zones by extending the company's VPC from eu-central-1 to the chosen Local Zone.**

### 🔍 해설

- AWS Local Zones는 특정 도시 근처에 위치해 단일 자릿수 밀리초 지연 시간을 제공

- 리전(eu-central-1)에 애플리케이션을 직접 배포하지 않고도, VPC를 Local Zone으로 확장해 규제 요구사항을 충족

## 회고

기본 개념을 숙지했다고 생각했지만 문제에 대입하니 적용하기 쉽지 않았다. 그래도 생각보다 중복되는 개념의 문제가 많아서 시험 자체는 중복되는 개념을 익히면 될 거 같다.
