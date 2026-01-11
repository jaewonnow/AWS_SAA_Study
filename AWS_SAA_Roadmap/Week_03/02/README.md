# Week03 - EC2

## Q14

### 🧩 문제 요약

ALB 뒤의 멀티 AZ Auto Scaling EC2 기반 이커머스에서 MySQL 8.0 DB를 EC2 한 대에 올려 쓰고 있는데 부하가 늘면 DB 성능이 급격히 떨어지고 읽기 요청이 쓰기보다 많아 예측 불가능한 읽기 트래픽을 자동으로 확장하면서도 고가용성을 유지해야 한다.

### ✅ 정답

**C. Use Amazon Aurora with a Multi-AZ deployment. Configure Aurora Auto Scaling with Aurora Replicas.**

### 🔍 정리

- 읽기 트래픽 확장은 Read Replica/Aurora Replica로 해결하는 게 정석이며, Aurora는 리드 레플리카를 빠르게 추가/제거 가능
- Aurora Auto Scaling은 변동이 큰 읽기 워크로드에 맞춰 Aurora Replicas 수를 자동 조절해 운영 부담을 줄임
- Multi-AZ로 고가용성을 유지하면서, 단일 EC2 DB에서 발생하는 병목/장애 리스크를 줄일 수 있음

## Q20

### 🧩 문제 요약

프로덕션 EC2의 EBS 볼륨에 있는 대용량 데이터를 같은 리전의 테스트 환경으로 빠르게 복제해야 하고 테스트에서 데이터 변경이 프로덕션에 영향을 주면 안 되며 복제된 데이터는 항상 높은 I/O 성능을 제공해야 한다.

### ✅ 정답

**D. Take EBS snapshots of the production EBS volumes. Turn on the EBS fast snapshot restore feature on the EBS snapshots. Restore the snapshots into new EBS volumes. Attach the new EBS volumes to EC2 instances in the test environment.**

### 🔍 정리

- EBS Fast Snapshot Restore(FSR) 는 스냅샷에서 새 볼륨 복원 시 초기화/워밍업 없이 즉시 높은 I/O 성능을 제공해 복제 시간을 크게 줄임
- 스냅샷에서 새 EBS 볼륨을 생성하면 테스트 환경의 변경이 프로덕션에 영향을 주지 않음(완전 분리)
- 일반 스냅샷 복원은 처음엔 성능이 낮아질 수 있어(지연 로딩) “일관된 고성능 I/O” 요구사항에 불리함

## Q24

### 🧩 문제 요약

최근 EC2 비용이 증가했으며 일부 EC2 인스턴스에서 원치 않는 수직 확장(인스턴스 타입 변경) 이 발생한 것으로 보인다. 최근 2개월간 EC2 비용을 인스턴스 타입 기준으로 비교 그래프를 만들고, 원인을 심층 분석하되 운영 오버헤드를 최소화해야 한다.

### ✅ 정답

**B. Use Cost Explorer's granular filtering feature to perform an in-depth analysis of EC2 costs based on instance types.**

### 🔍 정리

- Cost Explorer는 서비스/인스턴스 타입/기간별로 세밀한 필터링과 시각화를 즉시 제공 → 추가 구성 불필요
- 최근 2개월 비교 그래프와 인스턴스 타입별 비용 추적이 기본 기능으로 가능
- Budgets(A)는 경고/한도 관리용, 대시보드(C)는 심층 분석 한계, CUR+QuickSight(D)는 설정·운영 오버헤드 큼

## Q31

### 🧩 문제 요약

AWS에서 운영 중인 EC2, RDS, Redshift 리소스들이 필수 태그로 올바르게 설정되었는지 자동으로 확인해야 하며 이를 설정·운영 부담을 최소화하면서 구현하려고 한다.

### ✅ 정답

**A. Use AWS Config rules to define and detect resources that are not properly tagged.**

### 🔍 정리

- AWS Config는 리소스 구성 상태를 지속적으로 평가하는 관리형 서비스로, 태그 규칙을 손쉽게 적용 가능
- Managed Config Rules(예: required-tags)는 코드 작성 없이 바로 사용 → 운영 오버헤드 최소
- Cost Explorer는 비용 분석용이며 태그 누락 탐지는 목적에 부합하지 않음
- API/Lambda 방식은 커스텀 개발·유지보수가 필요해 관리 부담이 큼

## Q35

### 🧩 문제 요약

퍼블릭 웹 애플리케이션을 ELB 뒤의 EC2로 운영하고 있으며 DNS는 서드파티를 사용한다. 대규모 DDoS 공격을 탐지하고 보호할 수 있는 AWS 솔루션이 필요하다.

### ✅ 정답

**D. Enable AWS Shield Advanced and assign the ELB to it.**

### 🔍 정리

- AWS Shield Advanced는 L3/L4/L7 대규모 DDoS 공격에 대한 고급 보호 및 탐지를 제공
- ELB에 직접 연동해 DNS가 Route 53이 아니어도 보호 가능
- GuardDuty(A)는 위협 탐지(로그 분석)용, Inspector(B)는 취약점 점검용으로 DDoS 방어 목적과 다름
- Shield Standard는 기본 보호만 제공하며, Route 53을 쓰지 않는 환경에서는 Advanced가 요구사항에 더 적합

## Q84

### 🧩 문제 요약

프로덕션은 24시간 상시 운영되고, 개발/테스트는 하루 최소 8시간만 사용하며 사용하지 않을 때는 자동으로 중지할 계획인데, 전체 3티어 EC2 비용을 가장 효율적으로 줄일 수 있는 구매 옵션을 선택해야 한다.

### ✅ 정답

**B. Use Reserved Instances for the production EC2 instances. Use On-Demand Instances for the development and test EC2 instances.**

### 🔍 정리

- 상시(24/7) 운영 워크로드는 Reserved Instances(또는 Savings Plans) 로 가장 큰 비용 절감 효과를 얻음
- 가동 시간이 변동적이고 중지 가능한(dev/test) 환경은 On-Demand가 유리하며 실제 사용 시간만 비용이 발생하고 중지 시 과금이 줄어듦
- Spot/Spot block은 중단 위험이 있어 프로덕션 3티어에 부적합하고, “정해진 시간 보장”도 제한적이라 요구사항에 맞지 않음

## Q100

### 🧩 문제 요약

EC2에서 실행되는 컨테이너 앱이 다른 시스템과 통신하기 전에 보안 인증서를 내려받아야 하며, 인증서를 거의 실시간으로 안전하게 암·복호화하고 암호화된 데이터는 고가용성 스토리지에 저장하면서 운영 부담을 최소화해야 한다.

### ✅ 정답

**C. Create an AWS Key Management Service (AWS KMS) customer managed key. Allow the EC2 role to use the KMS key for encryption operations. Store the encrypted data on Amazon S3.**

### 🔍 정리

- KMS는 관리형 키 서비스로 실시간에 가까운 암·복호화를 안전하게 제공하며 운영 오버헤드가 가장 낮음
- S3는 기본적으로 고가용성/내구성 스토리지라 “암호화 후 저장” 요구사항에 적합
- EC2 역할(IAM Role)에 KMS 사용 권한을 부여하면 자격 증명 관리 없이 안전하게 접근 가능

## Q104

### 🧩 문제 요약

Windows 기반 EC2 웹 서버로 운영되는 웹사이트가 수천 개 IP에서 발생하는 대규모 DDoS 공격을 받아도 다운타임 없이 서비스를 유지해야 한다. (2개)

### ✅ 정답

**A. Use AWS Shield Advanced to stop the DDoS attack.**
**C. Configure the website to use Amazon CloudFront for both static and dynamic content.**

### 🔍 정리

- AWS Shield Advanced는 대규모 L3/L4/L7 DDoS에 대한 관리형 보호와 자동 완화, 가시성을 제공해 다운타임을 최소화

- CloudFront는 글로벌 엣지에서 트래픽을 흡수·분산하여 원본(EC2)으로 가는 공격 트래픽을 크게 줄임(정적/동적 모두 가속·보호)

- GuardDuty는 탐지용이며 자동 차단은 아님, Lambda로 NACL 갱신은 대규모 공격에 비효율적

- Spot 인스턴스 확장은 DDoS 완화책이 아니며 중단 위험 존재

## Q111

### 🧩 문제 요약

EC2에서 운영 중인 ActiveMQ 큐와 EC2 컨슈머, EC2의 MySQL로 구성된 메시지 처리 시스템을 AWS에서 가장 높은 가용성으로 만들되 운영 복잡도는 낮게 유지하고 싶다.

### ✅ 정답

**D. Use Amazon MQ with active/standby brokers configured across two Availability Zones. Add an Auto Scaling group for the consumer EC2 instances across two Availability Zones. Use Amazon RDS for MySQL with Multi-AZ enabled.**

### 🔍 정리

- Amazon MQ (Multi-AZ active/standby) 는 브로커를 관리형으로 제공해 EC2 직접 운영보다 가용성과 운영 편의가 높음
- 컨슈머는 ASG로 멀티 AZ 분산하면 인스턴스 장애·트래픽 변동에도 자동 복구/확장 가능
- DB는 RDS MySQL Multi-AZ 가 가장 표준적인 고가용성 구성으로 EC2 DB 복제보다 운영 복잡도가 낮고 장애 조치가 자동화됨

## Q115

### 🧩 문제 요약

퍼블릭 서브넷의 EC2 인스턴스가 S3에 있는 고객 데이터 파일을 인터넷을 통해 전송하고 있는데 파일 전송 트래픽이 인터넷을 거치지 않고 프라이빗 경로로만 이동하도록 네트워크 아키텍처를 변경해야 한다.

### ✅ 정답

**C. Move the EC2 instances to private subnets. Create a VPC endpoint for Amazon S3, and link the endpoint to the route table for the private subnets.**

### 🔍 정리

- S3로 인터넷 없이 프라이빗 접근하려면 S3 Gateway VPC Endpoint가 정석
- 프라이빗 경로 강제를 위해서는 EC2를 프라이빗 서브넷으로 이동시키고, 라우팅을 엔드포인트로 붙이는 구성이 가장 명확함
- NAT Gateway/보안그룹 제한은 인터넷 경로 자체를 없애지 못하고 Direct Connect는 과도하고 운영 부담이 큼

## Q130

### 🧩 문제 요약

ALB 뒤의 멀티 AZ Auto Scaling 그룹에서 실행되는 EC2 애플리케이션이 CPU 사용률 약 40%에서 가장 좋은 성능을 내며 모든 인스턴스의 성능을 이 수준으로 지속적으로 유지해야 한다.

### ✅ 정답

**B. Use a target tracking policy to dynamically scale the Auto Scaling group.**

### 🔍 정리

- Target Tracking Scaling은 원하는 지표(예: CPU 40%)를 목표값으로 유지하도록 자동으로 확장/축소
- 트래픽 변동에 즉각 반응하며 가장 표준적이고 운영 오버헤드가 낮은 방식
- Simple/Scheduled Scaling은 고정 규칙 기반으로 목표 유지에 부적합, Lambda 수동 제어는 불필요한 복잡성 증가

## Q138

### 🧩 문제 요약

현재 단일 AZ에서 EC2 기반 RabbitMQ 큐와 컨슈머 애플리케이션, 그리고 EC2 기반 PostgreSQL DB로 운영 중인데 장애 지점을 제거해 최고 가용성을 확보하면서도 운영 오버헤드를 최소화하도록 아키텍처를 재설계해야 한다.

### ✅ 정답

**B. Migrate the queue to a redundant pair (active/standby) of RabbitMQ instances on Amazon MQ. Create a Multi-AZ Auto Scaling group for EC2 instances that host the application. Migrate the database to run on a Multi-AZ deployment of Amazon RDS for PostgreSQL.**

### 🔍 정리

- 메시지 브로커는 EC2 직접 운영보다 Amazon MQ(Multi-AZ active/standby) 가 관리형이라 가용성과 운영 편의성이 높음
- 애플리케이션 계층은 Multi-AZ Auto Scaling으로 장애 시 자동 대체 및 확장 가능
- DB 계층은 EC2 DB를 Multi-AZ로 직접 운영하는 것보다 RDS Multi-AZ가 자동 장애 조치와 관리 부담 최소화에 최적

## Q145

### 🧩 문제 요약

단일 온디맨드 EC2 한 대에서 PHP 웹서버와 애플리케이션, MySQL DB까지 모두 돌리고 있어 트래픽이 몰릴 때 성능 저하와 5xx 에러가 발생하며 애플리케이션이 끊김 없이 자연스럽게 확장되도록 하면서 비용도 가장 효율적으로 줄여야 한다.

### ✅ 정답

**A. Migrate the database to an Amazon RDS for MySQL DB instance. Create an AMI of the web application. Use the AMI to launch a second EC2 On-Demand Instance. Use an Application Load Balancer to distribute the load to each EC2 instance.**

### 🔍 정리

- 단일 EC2에 웹+앱+DB를 같이 두면 병목이 생기므로, 먼저 DB를 RDS로 분리해 확장성과 안정성을 확보

- 웹/앱 계층은 ALB로 로드밸런싱해야 5xx를 줄이고 트래픽 증가에도 수평 확장이 가능

- Route 53 가중치 라우팅은 헬스체크/세션/트래픽 분산 측면에서 ALB보다 웹 확장에 덜 적합

- Spot Fleet 기반 ASG는 비용은 낮출 수 있지만 중단 가능성이 있어 “끊김 없는(seamless)” 요구에 불리하고 설계도 복잡해짐

## Q146

### 🧩 문제 요약

프로덕션에서 ALB 뒤의 온디맨드 EC2로 무상태 웹앱을 운영 중인데 평일 8시간은 트래픽이 매우 높고 밤에는 중간 수준으로 일정하며 주말에는 낮은 사용량을 보인다. 가용성을 해치지 않으면서 EC2 비용을 최소화해야 한다.

### ✅ 정답

**B. Use Reserved Instances for the baseline level of usage. Use Spot instances for any additional capacity that the application needs.**

### 🔍 정리

- Baseline(항상 필요한 최소 용량) 은 중단 없이 유지돼야 하므로 Reserved Instances로 비용을 절감하면서 안정적으로 확보

- 피크 시간 추가 용량은 무상태 앱이라 수평 확장이 쉬워 Spot으로 비용을 크게 줄일 수 있음

- 전체를 Spot으로 돌리면 중단 위험으로 가용성 영향 가능, Dedicated는 비용 증가

## Q251

### 🧩 문제 요약

프라이빗 서브넷에 있는 EC2 인스턴스가 외부 벤더의 월간 보안 업데이트를 다운로드해야 하지만 인터넷에 직접 노출되면 안 된다.

### ✅ 정답

**B. Create a NAT gateway, and place it in a public subnet. Configure the private subnet route table to use the NAT gateway as the default route.**

### 🔍 정리

- 프라이빗 서브넷의 아웃바운드 인터넷 접근은 NAT Gateway
- Internet Gateway는 퍼블릭 서브넷 전용
- NAT Instance는 운영 오버헤드 큼

## Q353

단일 AZ의 EC2에서 자체 운영 MySQL을 io2(1TB) EBS로 쓰고 있는데 피크에 읽기/쓰기가 각각 1,000 IOPS 수준이며 성능을 안정화하고 중단을 최소화하면서 비용도 줄이고 싶고 향후 IOPS를 2배까지 감당할 여유를 남기면서 DB를 고가용·내결함의 완전 관리형으로 옮기고 싶다.

### ✅ 정답

**B. Use a Multi-AZ deployment of an Amazon RDS for MySQL DB instance with a General Purpose SSD (gp2) EBS volume.**

### 🔍 정리

- 완전 관리형 + 고가용성/내결함 요구는 RDS Multi-AZ가 정석이며 장애 조치가 자동화돼 중단을 최소화함

- 요구 IOPS(현재 1,000, 향후 2,000)는 보통 **General Purpose SSD(gp2)**로도 충분히 커버 가능한 범위라, io2보다 비용 효율적

- io2/io2 Block Express는 초고 IOPS/초저지연이 필요한 경우에 주로 선택하므로, 이 수준의 IOPS에서는 과투자일 가능성이 큼

## 회고

EC2 문제를 골라서 풀었지만 타 개념을 더 많이 공부했다. 그만큼 EC2 는 기본적으로 알고 있어야하는 개념인 것 같다.
