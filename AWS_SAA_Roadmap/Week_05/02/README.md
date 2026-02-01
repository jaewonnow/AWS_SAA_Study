# Placeholder

# Week05 - RDS (multi-AZ) , Aurora , DynamoDB , Elasticcache

## Q138

### 🧩 문제 요약

단일 AZ에서 EC2 기반 RabbitMQ 큐 + EC2 컨슈머 애플리케이션 + EC2 PostgreSQL DB로 운영 중인데 최고 가용성을 확보하면서 운영 부담을 최소화하도록 재설계해야 한다.

### ✅ 정답

**B. Migrate the queue to a redundant pair (active/standby) of RabbitMQ instances on Amazon MQ. Create a Multi-AZ Auto Scaling group for EC2 instances that host the application. Migrate the database to run on a Multi-AZ deployment of Amazon RDS for PostgreSQL.**

### 🔍 정리

- 메시지 브로커는 관리형 서비스(Amazon MQ) 로 옮기면 멀티 AZ HA(Active/Standby)와 운영 부담 감소를 동시에 달성

- 애플리케이션 계층은 Multi-AZ ASG 로 장애 시 자동 대체/확장 가능

- DB는 RDS Multi-AZ 가 EC2 자체 복제/운영보다 장애조치 자동화로 운영 오버헤드가 가장 낮고 HA에 최적

## Q178

### 🧩 문제 요약

단일 리전에 EC2와 RDS를 운영 중이고 다른 리전으로 백업을 복제해야 한다. 목표는 운영 오버헤드를 최소화하는 것이다.

### ✅ 정답

**A. Use AWS Backup to copy EC2 backups and RDS backups to the separate Region.**

### 🔍 정리

- EC2와 RDS 백업은 AWS Backup으로 통합 관리 → 리소스별 백업 정책을 한 곳에서 설정 가능하며 교차 리전 복제 지원

AWS Backup은 자동 스케줄링 + 중앙집중 관리 제공 → DLM/스냅샷/AMI 개별 관리 대비 운영 부담 최소

- 별도 AMI 생성, 스냅샷 수동 복제, S3 CRR 구성 없이 관리형 서비스로 백업 복제 자동화 가능

`교차 리전 백업 + 최소 운영 오버헤드 = AWS Backup`

## Q182

온프레미스 MySQL DB를 AWS로 마이그레이션하면서 장애 재발 방지, 데이터 손실 최소화, 모든 트랜잭션을 최소 2개 노드에 동기 저장해야 한다.

### ✅ 정답

**B. Create an Amazon RDS MySQL DB instance with Multi-AZ functionality enabled to synchronously replicate the data.**

### 🔍 정리

- MySQL DB를 Amazon RDS Multi-AZ 사용하면 Primary–Standby 간 동기식 복제로 트랜잭션마다 최소 2개 노드에 기록

- Multi-AZ는 자동 장애조치(Failover) 제공 → 장애 시 수동 개입 없이 서비스 지속 가능

- Read Replica는 비동기 복제이므로 데이터 손실 가능
- EC2 기반 MySQL + Lambda 복제는 운영 복잡도 증가 및 HA 보장 어려움

`동기 복제 + 최소 데이터 손실 + 운영 오버헤드 최소 = RDS MySQL Multi-AZ`

## Q187

로드밸런싱된 프런트엔드 + 컨테이너 기반 앱 + 관계형 DB로 이커머스 서비스를 구축해야 하며 고가용성과 최소 수동 개입(운영 자동화/관리형)이 목표다. (2개 선택)

### ✅ 정답

**A. Create an Amazon RDS DB instance in Multi-AZ mode.**

**D. Create an Amazon Elastic Container Service (Amazon ECS) cluster with a Fargate launch type to handle the dynamic application load.**

### 🔍 정리

- DB는 RDS Multi-AZ → 동기 복제 + 자동 장애조치로 HA 확보, DB 운영(복제/Failover) 수동 개입 최소

- 컨테이너 앱은 ECS Fargate → EC2 노드(서버) 관리 없이 자동 확장/운영 가능, 클러스터 운영 오버헤드 최소

## Q193

EC2에서 배치 애플리케이션을 실행 중이며 여러 RDS DB에 대한 읽기 트래픽이 과다하다. DB 읽기 수를 줄이면서 고가용성을 유지해야 한다.

### ✅ 정답

**D. Use Amazon ElastiCache for Memcached.**

### 🔍 정리

- DB 앞단에 ElastiCache for Memcached를 캐시 계층으로 추가하면 반복적인 읽기 요청을 캐시에서 처리해 DB Read 부하 대폭 감소

- ElastiCache는 관리형 인메모리 캐시로 멀티 노드/멀티 AZ 구성 가능해 캐시 계층에서도 고가용성 확보

- Memcached는 단순 키-값 캐시 + 수평 확장에 최적, Redis 대비 설정·운영 부담이 낮아 배치/읽기 위주 워크로드에 적합

`읽기 트래픽 감소 + 운영 오버헤드 최소 + HA = ElastiCache for Memcached`

## Q241

### 🧩 문제 요약

PostgreSQL 학생 기록 DB를 AWS로 마이그레이션하며 항상 여러 리전에서 온라인 상태로 데이터 접근 가능해야 한다. 운영 오버헤드는 최소여야 한다.

### ✅ 정답

**C. Migrate the PostgreSQL database to an Amazon RDS for PostgreSQL DB instance. Create a read replica in another Region.**

### 🔍 정리

- PostgreSQL은 Amazon RDS for PostgreSQL로 이전해 관리형 DB로 패치/백업/모니터링 등 운영 부담 최소

- 다른 리전에 Read Replica 구성 → 기본 리전 장애/네트워크 이슈가 있어도 타 리전에서 DB를 온라인으로 조회 가능(멀티 리전 가용성)

## Q268

### 🧩 문제 요약

EC2 + ALB 기반 웹앱이 점수 데이터를 RDS MySQL에 저장 중인데 읽기 성능 저하로 지연/끊김이 발생한다. 사용자 경험을 개선하되 아키텍처 변경은 최소화해야 한다.

### ✅ 정답

**A. Use Amazon ElastiCache in front of the database.**

### 🔍 정리

- DB 읽기 병목은 ElastiCache(주로 Redis/Memcached) 캐시 계층 추가로 해결 → 자주 조회되는 점수 데이터를 캐시에서 응답해 RDS Read 부하 감소

- 캐시는 애플리케이션 구조를 크게 바꾸지 않고(DB 앞단 추가) 성능 개선 효과가 큼

## Q273

### 🧩 문제 요약

단일 리전 운영 중인 이커머스가 다른 리전을 포함한 DR을 구축해야 한다. DR 리전의 DB는 최소 지연으로 최신 상태여야 하고 DR 인프라는 축소 용량으로 상시 운영하다가 필요 시 확장해야 한다. 목표는 최저 RTO다.

### ✅ 정답

**B. Use an Amazon Aurora global database with a warm standby deployment.**

### 🔍 정리

- DB는 Aurora Global Database으로 리전 간 저지연 복제로 DR 리전 DB를 거의 최신 상태로 유지(업투데이트 요구 충족)

- DR 인프라는 Warm Standby으로 DR 리전에 축소 용량으로 상시 구동해 두고, 장애 시 빠르게 스케일 업 가능 → Pilot Light보다 RTO가 낮음

## Q276

EC2 ASG + RDS Oracle(PL/SQL 사용) 구조에서 트래픽 증가로 EC2 과부하 + RDS 스토리지 부족이 발생한다. 트래픽은 꾸준하지만 예측 불가하게 증가하다가 언젠가 평탄화될 전망이며 시스템이 자동으로 확장되도록 해야 한다. (2개 선택)

### ✅ 정답

**A. Configure storage Auto Scaling on the RDS for Oracle instance.**
**D. Configure the Auto Scaling group to use the average CPU as the scaling metric.**

### 🔍 정리

- DB 스토리지는 RDS for Oracle Storage Auto Scaling이면 스토리지 부족을 자동으로 확장해 운영 개입 없이 용량 문제 해결

- 애플리케이션 계층은 ASG에 평균 CPU 기반 타깃 추적/스케일링 정책 적용하면 트래픽 증가로 인한 EC2 과부하를 자동으로 완화

## Q458

### 🧩 문제 요약

API Gateway로 REST API를 구성하며 컴퓨팅 리소스는 메모리 1GB + 스토리지 2GB가 필요하다. 데이터는 관계형(Relational) 형식이어야 하며, 운영/관리 부담이 최소여야 한다. (2개 선택)

### ✅ 정답

**B. AWS Lambda**
**C. Amazon RDS**

### 🔍 정리

- 컴퓨팅 계층은 AWS Lambda → 1GB 메모리 충족 가능 + 임시 스토리지(/tmp) 확장으로 2GB 저장공간 요구 충족, 서버 관리 없이 운영 오버헤드 최소

- 데이터 계층은 Amazon RDS → 관리형 관계형 DB로 백업/패치/HA 옵션 제공, 직접 운영(EC2/쿠버네티스) 대비 관리 부담 최소

- (배제 이유) DynamoDB는 NoSQL이라 “관계형 데이터” 요구사항 불충족

- (배제 이유) EC2/EKS는 서버/클러스터 운영이 필요해 관리 effort 증가

## Q537

### 🧩 문제 요약

3AZ에 걸친 3-티어 웹앱(ALB + 세션을 로컬에 들고 있는 EC2 웹서버 + EC2 MySQL)이 있고, 트래픽이 급증할 수 있다. 수평 확장과 3AZ 고가용성을 동시에 만족해야 한다.

### ✅ 정답

**A. Migrate the MySQL database to Amazon RDS for MySQL with a Multi-AZ DB cluster deployment. Use Amazon ElastiCache for Redis with high availability to store session data and to cache reads. Migrate the web server to an Auto Scaling group that is in three Availability Zones.**

### 🔍 정리

- DB는 RDS for MySQL Multi-AZ DB cluster → AZ 장애에도 자동 복구/Failover로 3AZ 고가용성 확보 + EC2 DB 운영 부담 제거

- 세션/캐시는 ElastiCache for Redis(HA) → 웹서버 로컬 세션을 외부로 분리해 ASG 수평 확장 시에도 세션 유지 + Redis는 Multi-AZ/Failover로 HA에 적합

- 웹서버는 3AZ Auto Scaling Group → 트래픽 급증 시 자동 확장, AZ 장애 시 자동 대체로 가용성 확보

- Memcached는 장애조치/내구성 측면에서 세션 저장용 HA 구성이 Redis보다 불리, DynamoDB는 관계형 MySQL 대체가 아님, Single-AZ RDS는 HA 불충족

## Q14

### 🧩 문제 요약

EC2 ASG(멀티 AZ) + ALB 기반 이커머스에서 트랜잭션 데이터는 EC2 단일 인스턴스 MySQL 8.0에 저장 중이다. 부하가 증가하면 DB 성능이 급격히 저하되고 읽기 요청이 쓰기보다 훨씬 많다. 예측 불가한 읽기 워크로드에 맞춰 DB가 자동 확장되고 고가용성도 유지해야 한다.

### ✅ 정답

**C. Use Amazon Aurora with a Multi-AZ deployment. Configure Aurora Auto Scaling with Aurora Replicas.**

### 🔍 정리

- DB는 Amazon Aurora Multi-AZ → 관리형 HA(자동 장애조치)로 EC2 단일 DB 대비 가용성/성능 안정성 확보

- 읽기 확장은 Aurora Replicas + Aurora Auto Scaling → 예측 불가한 Read 트래픽에 맞춰 리더/리더가 아닌 리더(Reader) 인스턴스 수를 자동 증감

## Q90

### 🧩 문제 요약

공개 영화 데이터를 저장하는 RDS Single-AZ SQL DB가 있고 매일 랜덤 간격으로 실행되는 스크립트가 신규 영화 수 집계 쿼리를 돌린다. 스크립트가 돌 때 DB 성능 저하로 개발 작업이 방해된다. 운영 오버헤드 최소로 해결해야 한다.

### ✅ 정답

**B. Create a read replica of the database. Configure the script to query only the read replica.**

### 🔍 정리

- 집계 스크립트는 Read-only 워크로드 → RDS Read Replica로 읽기 트래픽을 분리하면 프로덕션/개발 쿼리와 충돌 감소

- Read Replica는 관리형 복제로 구성 간단 → 스크립트 대상만 Replica로 바꾸면 아키텍처 변경 최소 + 운영 부담 낮음

- Multi-AZ는 HA 목적(동기 복제/Failover)이라 성능 분리 효과가 제한적이고 비용 대비 요구사항과 방향이 다름

## Q300

온프레미스 레거시 앱을 AWS로 이전해야 하며, 앱은 24/7 상시 운영된다. 또한 DB 스토리지가 지속적으로 증가한다. 가장 비효율적인 선택을 고르시오.

### ✅ 정답

**C. Migrate the application layer to Amazon EC2 Reserved Instances. Migrate the data storage layer to Amazon Aurora Reserved Instances.**

### 🔍 정리

- 애플리케이션 계층은 EC2 Reserved Instances → 24/7 고정 사용 패턴에 최적(온디맨드 대비 비용 절감)

- 데이터 계층은 Aurora Reserved Instances → 상시 구동되는 관계형 DB 비용을 예약으로 절감 + 스토리지 자동 확장으로 성장하는 DB 스토리지 요구에 적합

- Spot은 중단 가능성이 있어 24/7 레거시 서비스에 부적합

- RDS/Aurora를 On-Demand로 두면 상시 운영 비용이 불리해 “MOST cost-effective”에 밀림

## Q518

### 🧩 문제 요약

Amazon RDS MySQL DB 인스턴스의 디스크 공간이 부족해지고 있다. 다운타임 없이 용량을 늘려야 하며 운영 effort는 최소여야 한다.

### ✅ 정답

**A. Enable storage autoscaling in RDS**

### 🔍 정리

- DB 스토리지는 RDS Storage Auto Scaling 활성화 → 사용량 증가 시 자동으로 스토리지 확장, 다운타임 없이 해결

- 관리형 기능으로 수동 개입·운영 작업 최소화 → 요구사항(LEAST effort) 충족
