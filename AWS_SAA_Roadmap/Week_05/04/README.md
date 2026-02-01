# Placeholder
## Q1(pdf Q#138)
한 회사가 AWS에서 전자상거래 애플리케이션을 운영하고 있습니다. 모든 신규 주문은 단일 가용 영역에 있는 Amazon EC2 인스턴스에서 실행되는 RabbitMQ 큐에 메시지로 게시됩니다.
이 메시지들은 다른 EC2 인스턴스에서 실행되는 다른 애플리케이션에 의해 처리됩니다.
이 애플리케이션은 주문 세부 정보를 또 다른 EC2 인스턴스의 PostgreSQL 데이터베이스에 저장합니다. 모든 EC2 인스턴스는 동일한 가용 영역에 있습니다.
이 회사는 최소한의 운영 오버헤드로 최고의 가용성을 제공할 수 있도록 아키텍처를 재설계해야 합니다.
이러한 요구 사항을 충족하기 위해 솔루션 아키텍트는 무엇을 해야 할까요?

A. 큐를 Amazon MQ의 RabbitMQ 인스턴스 이중화 쌍(액티브/스탠바이)으로 마이그레이션합니다. 애플리케이션을 호스팅하는 EC2 인스턴스에 대해 다중 가용 영역(Multi-AZ) Auto Scaling 그룹을 생성합니다.
PostgreSQL 데이터베이스를 호스팅하는 EC2 인스턴스에 대해 또 다른 다중 가용 영역 Auto Scaling 그룹을 생성합니다.
B. 큐를 Amazon MQ의 RabbitMQ 인스턴스 이중화 쌍(액티브/스탠바이)으로 마이그레이션합니다. 애플리케이션을 호스팅하는 EC2 인스턴스에 대해 다중 가용 영역 Auto Scaling 그룹을 생성합니다.
데이터베이스를 Amazon RDS for PostgreSQL의 다중 가용 영역 배포에서 실행되도록 마이그레이션합니다.
C. RabbitMQ 큐를 호스팅하는 EC2 인스턴스에 대해 다중 가용 영역 Auto Scaling 그룹을 생성합니다. 애플리케이션을 호스팅하는 EC2 인스턴스에 대해 또 다른 다중 가용 영역 Auto Scaling 그룹을 생성합니다. 데이터베이스를 Amazon RDS for PostgreSQL의 다중 가용 영역 배포에서 실행되도록 마이그레이션합니다.
D. RabbitMQ 큐를 호스팅하는 EC2 인스턴스에 대해 다중 가용 영역 Auto Scaling 그룹을 생성합니다. 애플리케이션을 호스팅하는 EC2 인스턴스를 위해 또 다른 멀티 AZ 오토 스케일링 그룹을 생성합니다.
PostgreSQL 데이터베이스를 호스팅하는 EC2 인스턴스를 위해 세 번째 멀티 AZ 오토 스케일링 그룹을 생성합니다.

메시지 큐	   Amazon MQ (관리형 RabbitMQ) Active/Standby 자동 관리
애플리케이션	Multi-AZ Auto Scaling Group
데이터베이스	Amazon RDS Multi-AZ 자동 장애 조치, 백업/패치 자동, 운영 부담 최소

정답 : B
## Q2(pdf Q#178)
한 회사의 인프라는 단일 AWS 리전에 있는 Amazon EC2 인스턴스와 Amazon RDS DB 인스턴스로 구성되어 있습니다. 이 회사는 데이터를 다른 리전에 백업하려고 합니다.
다음과 같은 솔루션 중 운영 오버헤드가 가장 적은 솔루션은 무엇입니까?

A. AWS Backup을 사용하여 EC2 백업과 RDS 백업을 다른 리전으로 복사합니다.
B. Amazon Data Lifecycle Manager(Amazon DLM)를 사용하여 EC2 백업과 RDS 백업을 다른 리전으로 복사합니다.
C. EC2 인스턴스의 Amazon Machine Image(AMI)를 생성합니다. 생성된 AMI를 다른 리전으로 복사합니다. RDS DB 인스턴스에 대한 읽기 복제본을 다른 리전에 생성합니다.
D. Amazon Elastic Block Store(Amazon EBS) 스냅샷을 생성합니다. 생성된 EBS 스냅샷을 다른 리전으로 복사합니다. RDS 스냅샷을 생성합니다.
RDS 스냅샷을 Amazon S3로 내보냅니다. S3 교차 리전 복제(CRR)를 다른 리전으로 구성합니다.

AWS Backup : EC2, EBS, RDS 통합 백업 서비스
스케줄, 보존 정책, 암호화, 자동화 모두 관리형
Cross-Region backup 복사 지원

설정 한번만 해두면 끝난다

가장 단순한 방법 + 가장 관리형

정답 : A
## Q3(pdf Q#182)
한 회사가 온프레미스 MySQL 데이터베이스를 AWS로 마이그레이션하려고 합니다. 이 회사는 최근 데이터베이스 장애를 경험했으며,
이로 인해 비즈니스에 상당한 영향을 받았습니다. 이러한 일이 재발하지 않도록 하기 위해, 회사는 AWS에서 다음과 같은 조건을 충족하는 안정적인 데이터베이스 솔루션을 원합니다.
데이터 손실을 최소화하고 모든 트랜잭션을 최소 두 개의 노드에 저장합니다.
다음 중 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

A. 세 개의 가용 영역에 있는 세 개의 노드에 동기 복제하는 Amazon RDS DB 인스턴스를 생성합니다.
B. 데이터를 동기적으로 복제하기 위해 Multi-AZ 기능이 활성화된 Amazon RDS MySQL DB 인스턴스를 생성합니다.
C. Amazon RDS MySQL DB 인스턴스를 생성한 다음, 데이터를 동기적으로 복제하는 별도의 AWS 리전에 읽기 복제본을 생성합니다.
D. MySQL 엔진이 설치된 Amazon EC2 인스턴스를 생성하고, AWS Lambda 함수를 실행하여 데이터를 Amazon RDS MySQL DB 인스턴스로 동기적으로 복제합니다.

온프레미스 → AWS 마이그레이션
모든 트랜잭션이 최소 2개 노드에 저장 -> 동기식 복제(synchronous replication)

RDS Multi-AZ
    Primary + Standby
    동기식 복제
    AZ 장애 시 자동 장애 조치

모든 커밋:
최소 2개 노드에 기록 후 성공 처리

정답 : B
## Q4(pdf Q#187)
한 회사가 로드 밸런싱 프런트엔드, 컨테이너 기반 애플리케이션, 관계형 데이터베이스로 구성된 전자상거래 애플리케이션을 개발 중입니다.
솔루션 아키텍트는 수동 개입을 최소화하면서 고가용성을 갖춘 솔루션을 구축해야 합니다.
다음 중 이러한 요구 사항을 충족하는 솔루션은 무엇입니까? (두 가지를 선택하십시오.)

A. Multi-AZ 모드로 Amazon RDS DB 인스턴스를 생성합니다.
B. 다른 가용 영역에 Amazon RDS DB 인스턴스와 하나 이상의 복제본을 생성합니다.
C. 동적 애플리케이션 로드를 처리하기 위해 Amazon EC2 인스턴스 기반 Docker 클러스터를 생성합니다.
D. 동적 애플리케이션 로드를 처리하기 위해 Fargate 시작 유형의 Amazon Elastic Container Service(Amazon ECS) 클러스터를 생성합니다.
E. 동적 애플리케이션 로드를 처리하기 위해 Amazon EC2 시작 유형의 Amazon Elastic Container Service(Amazon ECS) 클러스터를 생성합니다.

DB 고가용성 + 자동 장애 조치 → RDS Multi-AZ
컨테이너 + 운영 최소화 → ECS Fargate

정답 : A, D
## Q5(pdf Q#193)
한 회사가 Amazon EC2 인스턴스에서 배치 애플리케이션을 실행하고 있습니다. 이 애플리케이션은 여러 개의 Amazon RDS 데이터베이스를 사용하는 백엔드로 구성되어 있습니다.
이 애플리케이션으로 인해 데이터베이스에 대한 읽기 요청이 과도하게 발생하고 있습니다. 솔루션 아키텍트는 고가용성을 보장하면서 데이터베이스 읽기 횟수를 줄여야 합니다.
솔루션 아키텍트는 이 요구 사항을 충족하기 위해 무엇을 해야 할까요?

A. Amazon RDS 읽기 복제본을 추가합니다.
B. Amazon ElastiCache for Redis를 사용합니다.
C. Amazon Route 53 DNS 캐싱을 사용합니다.
D. Amazon ElastiCache for Memcached를 사용합니다.

인메모리 캐시 → DB 읽기 대폭 감소
Redis 특징: Multi-AZ
복제(replication)
자동 장애 조치

정답 : B
## Q6(pdf Q#241)
온라인 교육 회사가 AWS 클라우드로 이전하고 있습니다. 이 회사는 학생 기록을 PostgreSQL 데이터베이스에 저장하고 있습니다.
이 회사는 여러 AWS 리전에서 항상 데이터에 접근 가능하고 온라인 상태인 솔루션이 필요합니다.
다음 중 운영 오버헤드를 최소화하면서 이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

A. PostgreSQL 데이터베이스를 Amazon EC2 인스턴스의 PostgreSQL 클러스터로 마이그레이션합니다.
B. PostgreSQL 데이터베이스를 Multi-AZ 기능이 활성화된 Amazon RDS for PostgreSQL DB 인스턴스로 마이그레이션합니다.
C. PostgreSQL 데이터베이스를 Amazon RDS for PostgreSQL DB 인스턴스로 마이그레이션하고, 다른 리전에 읽기 복제본을 생성합니다.
D. PostgreSQL 데이터베이스를 Amazon RDS for PostgreSQL DB 인스턴스로 마이그레이션하고, 데이터베이스 스냅샷을 다른 리전으로 복사하도록 설정합니다.

다른 리전에 리드 레플리카 생성
리전 장애 시:
레플리카를 승격(promote)하여 사용 가능
RDS 관리형 기능: 백업, 복제, 패치 자동

항상 온라인 조건에 잘 맞음

정답 : C
## Q7(pdf Q#268)
한 게임 회사가 점수를 표시하는 웹 애플리케이션을 운영하고 있습니다. 이 애플리케이션은 Application Load Balancer 뒤의 Amazon EC2 인스턴스에서 실행됩니다.
데이터는 Amazon RDS for MySQL 데이터베이스에 저장됩니다. 최근 데이터베이스 읽기 성능 문제로 인해 사용자들이 긴 지연과 끊김 현상을 경험하기 시작했습니다.
이 회사는 애플리케이션 아키텍처 변경을 최소화하면서 사용자 경험을 개선하고자 합니다.
이러한 요구 사항을 충족하기 위해 솔루션 아키텍트는 무엇을 해야 할까요?

A. 데이터베이스 앞에 Amazon ElastiCache를 사용합니다.
B. 애플리케이션과 데이터베이스 사이에 RDS Proxy를 사용합니다.
C. 애플리케이션을 EC2 인스턴스에서 AWS Lambda로 마이그레이션합니다.
D. 데이터베이스를 Amazon RDS for MySQL에서 Amazon DynamoDB로 마이그레이션합니다.

Amazon ElastiCache
AWS 관리형 인메모리 캐시 서비스

메모리 기반 → 초저지연(ms 단위)
DB 앞단에 배치
자주 조회되는 데이터 저장

효과
DB read 요청 감소
응답 속도 대폭 향상
DB 부하 감소

정답 : A
## Q8(pdf Q#273)
빠르게 성장하는 전자상거래 회사가 단일 AWS 리전에서 워크로드를 실행하고 있습니다. 솔루션 아키텍트는 다른 AWS 리전을 포함하는 재해 복구(DR) 전략을 수립해야 합니다.
이 회사는 DR 리전에서 데이터베이스를 최대한 낮은 지연 시간으로 최신 상태로 유지하기를 원합니다.
DR 리전의 나머지 인프라는 용량을 줄여 실행해야 하며, 필요한 경우 확장할 수 있어야 합니다.
다음 중 가장 낮은 복구 시간 목표(RTO)로 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

A. 파일럿 라이트 배포를 사용하는 Amazon Aurora 글로벌 데이터베이스
B. 웜 스탠바이 배포를 사용하는 Amazon Aurora 글로벌 데이터베이스
C. 파일럿 라이트 배포를 사용하는 Amazon RDS Multi-AZ DB 인스턴스
D. 웜 스탠바이 배포를 사용하는 Amazon RDS Multi-AZ DB 인스턴스

RTO (Recovery Time Objective)

장애 발생 후 서비스 복구까지 걸리는 시간
낮을수록 좋음
“얼마나 빨리 다시 서비스하느냐”

RPO (Recovery Point Objective)

얼마나 최신 데이터까지 복구되느냐
RPO ≈ 0 → 데이터 손실 거의 없음

Amazon Aurora Global Database

하나의 Primary Region
여러 Secondary Region

특징: 스토리지 레벨 복제
지연 1초 미만
거의 실시간 동기화

정답 : B
## Q9(pdf Q#276)
한 회사가 Auto Scaling 그룹의 여러 Amazon EC2 인스턴스에 배포된 다계층 애플리케이션을 운영하고 있습니다. Amazon RDS for Oracle 인스턴스는
이 애플리케이션의 데이터 계층으로, Oracle 전용 PL/SQL 함수를 사용합니다. 애플리케이션 트래픽이 꾸준히 증가하고 있으며, 이로 인해
EC2 인스턴스가 과부하되고 RDS 인스턴스의 저장 공간이 부족해지고 있습니다. Auto Scaling 그룹에는 스케일링 메트릭이 없고
최소 정상 인스턴스 수만 정의되어 있습니다. 회사는 트래픽이 안정되기 전까지 일정하지만 예측 불가능한 속도로 계속 증가할 것으로 예상합니다.
솔루션 아키텍트는 증가하는 트래픽에 맞춰 시스템이 자동으로 확장될 수 있도록 어떤 조치를 취해야 할까요? (두 가지를 선택하세요.)

A. RDS for Oracle 인스턴스에 스토리지 Auto Scaling을 구성합니다.
B. Auto Scaling 스토리지를 사용하기 위해 데이터베이스를 Amazon Aurora로 마이그레이션합니다.
C. RDS for Oracle 인스턴스에 사용 가능한 저장 공간 부족에 대한 알람을 구성합니다.
D. 자동 스케일링 그룹이 평균 CPU를 스케일링 지표로 사용하도록 구성합니다.
E. 자동 스케일링 그룹이 평균 사용 가능한 메모리를 스케일링 지표로 사용하도록 구성합니다.

Storage Auto Scaling : RDS 스토리지가 자동으로 증가
수동 확장 X
스토리지 부족으로 인한 장애 방지

Auto Scaling Metric : “언제 인스턴스를 늘리거나 줄일지” 판단하는 기준

대표적인 메트릭: CPU 사용률
네트워크
요청 수

정답 : A, D
## Q10(pdf Q#458)
솔루션 아키텍트가 현금 상환 서비스를 위한 REST API를 Amazon API Gateway에서 설계하고 있습니다. 이 애플리케이션은 컴퓨팅 리소스로 1GB의 메모리와 2GB의 스토리지가 필요합니다. 데이터는 관계형 형식이어야 합니다.
다음 중 관리 노력이 가장 적게 드는 AWS 서비스 조합은 무엇입니까? (두 가지를 선택하십시오.)
A. Amazon EC2
B. AWS Lambda
C. Amazon RDS
D. Amazon DynamoDB
E. Amazon Elastic Kubernetes Services (Amazon EKS)

정답 : B, C
## Q11(pdf Q#537)
한 회사가 AWS 클라우드의 세 개 가용 영역에서 운영되는 3계층 웹 애플리케이션을 사용하고 있습니다. 애플리케이션 아키텍처는
애플리케이션 로드 밸런서, 사용자 세션 상태를 저장하는 Amazon EC2 웹 서버, 그리고 EC2 인스턴스에서 실행되는 MySQL 데이터베이스로 구성됩니다.
이 회사는 애플리케이션 트래픽이 갑자기 증가할 것으로 예상하고 있습니다. 따라서 향후 애플리케이션 용량 수요에 맞춰 확장할 수 있어야 하며,
세 개 가용 영역 모두에서 고가용성을 보장해야 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

A. MySQL 데이터베이스를 다중 가용 영역(AZ) DB 클러스터 배포를 사용하는 Amazon RDS for MySQL로 마이그레이션합니다. 고가용성을 지원하는 Amazon ElastiCache for Redis를 사용하여 세션 데이터를 저장하고 읽기 캐시를 수행합니다. 웹 서버를 3개의 가용 영역에 걸쳐 있는 Auto Scaling 그룹으로 마이그레이션합니다.
B. MySQL 데이터베이스를 다중 가용 영역(AZ) DB 클러스터 배포를 사용하는 Amazon RDS for MySQL로 마이그레이션합니다. 고가용성을 지원하는 Amazon ElastiCache for Memcached를 사용하여 세션 데이터를 저장하고 읽기 캐시를 수행합니다. 웹 서버를 3개의 가용 영역에 걸쳐 있는 Auto Scaling 그룹으로 마이그레이션합니다.
C. MySQL 데이터베이스를 Amazon DynamoDB로 마이그레이션합니다. DynamoDB Accelerator(DAX)를 사용하여 읽기 캐시를 수행합니다. 세션 데이터를 DynamoDB에 저장합니다. 웹 서버를 3개의 가용 영역에 걸쳐 있는 Auto Scaling 그룹으로 마이그레이션합니다.
D. MySQL 데이터베이스를 단일 가용 영역에 있는 Amazon RDS for MySQL로 마이그레이션합니다. 고가용성을 지원하는 Amazon ElastiCache for Redis를 사용하여 세션 데이터를 저장하고 읽기 작업을 캐싱합니다. 웹 서버를 3개의 가용 영역에 분산된 Auto Scaling 그룹으로 마이그레이션합니다.

Multi-AZ DB Cluster : 여러 AZ에 걸쳐 데이터 분산
Writer + Reader 노드 구조
자동 장애 조치
높은 가용성 + 읽기 확장

Redis를 세션 저장소로 쓰는 이유

사용자 세션을 웹 서버에서 분리
인메모리 → 매우 빠름

Redis : Multi-AZ 지원
Replication
Automatic failover

ASG의 역할
트래픽 증가 → 자동으로 EC2 증가
AZ 장애 → 다른 AZ에서 자동 보충
ALB와 자연스럽게 연동

정답 : A
## Q12(pdf Q#14)
한 회사가 애플리케이션 로드 밸런서(ALB) 뒤의 Amazon EC2 인스턴스에서 전자상거래 애플리케이션을 운영하고 있습니다. 이 인스턴스들은 여러 가용 영역에 걸쳐 Amazon EC2
Auto Scaling 그룹에서 실행됩니다. Auto Scaling 그룹은 CPU 사용률 지표를 기반으로 확장됩니다. 전자상거래
애플리케이션은 대규모 EC2 인스턴스에 호스팅된 MySQL 8.0 데이터베이스에 거래 데이터를 저장합니다.
애플리케이션 부하가 증가함에 따라 데이터베이스 성능이 빠르게 저하됩니다. 애플리케이션은 쓰기 트랜잭션보다 읽기 요청을 더 많이 처리합니다.
이 회사는 고가용성을 유지하면서 예측 불가능한 읽기 워크로드의 수요를 충족하기 위해 데이터베이스를 자동으로 확장하는 솔루션을 원합니다.
어떤 솔루션이 이러한 요구 사항을 충족할까요?

A. 리더 및 컴퓨팅 기능을 위해 단일 노드를 사용하는 Amazon Redshift를 사용합니다.
B. 단일 가용 영역 배포를 사용하는 Amazon RDS를 사용하고, 다른 가용 영역에 리더 인스턴스를 추가하도록 Amazon RDS를 구성합니다.
C. 다중 가용 영역 배포를 사용하는 Amazon Aurora를 사용하고, Aurora 복제본을 사용하여 Aurora Auto Scaling을 구성합니다.
D. EC2 스팟 인스턴스에서 Memcached용 Amazon ElastiCache를 사용합니다.

Amazon Aurora: MySQL/PostgreSQL 호환 관리형 관계형 DB
기존 RDS보다:
성능 ↑
확장성 ↑
가용성 ↑

Aurora Multi-AZ 아키텍처
스토리지를 3개 AZ에 6-way 복제
기본적으로 고가용성 내장
Writer 1개 + Reader 여러 개 구조
-> AZ 하나 장애 나도 서비스 지속

정답 : C
## Q13(pdf Q#16)
한 회사가 AWS에 데이터 레이크를 호스팅하고 있습니다. 데이터 레이크는 Amazon S3와 Amazon RDS for PostgreSQL에 저장된 데이터로 구성됩니다. 이 회사는 데이터 레이크 내의 모든 데이터 소스를 포함하고 데이터 시각화를 제공하는 보고 솔루션이 필요합니다.
회사 경영진만 모든 시각화 자료에 대한 전체 액세스 권한을 가져야 하며, 나머지 직원들은 제한된 액세스 권한만 가져야 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

A. Amazon QuickSight에서 분석을 생성합니다. 모든 데이터 소스를 연결하고 새 데이터 세트를 생성합니다. 데이터를 시각화하는 대시보드를 게시합니다.
적절한 IAM 역할과 대시보드를 공유합니다.
B. Amazon QuickSight에서 분석을 생성합니다. 모든 데이터 소스를 연결하고 새 데이터 세트를 생성합니다. 데이터를 시각화하는 대시보드를 게시합니다.
적절한 사용자 및 그룹과 대시보드를 공유합니다.
C. Amazon S3의 데이터에 대한 AWS Glue 테이블과 크롤러를 생성합니다. AWS Glue ETL(추출, 변환, 로드) 작업을 생성하여 보고서를 생성합니다.
보고서를 Amazon S3에 게시합니다. S3 버킷 정책을 사용하여 보고서에 대한 액세스를 제한합니다.
D. Amazon S3에 있는 데이터에 대한 AWS Glue 테이블과 크롤러를 생성합니다. Amazon Athena 페더레이션 쿼리를 사용하여 Amazon RDS(PostgreSQL용) 내의 데이터에 액세스합니다.
Amazon Athena를 사용하여 보고서를 생성합니다. 보고서를 Amazon S3에 게시합니다. S3 버킷 정책을 사용하여 보고서에 대한 액세스를 제한합니다.

Amazon QuickSight : 
AWS의 완전 관리형 BI(비즈니스 인텔리전스) 서비스

다양한 데이터 소스 연결: S3
RDS
Athena
Redshift 등

QuickSight의 접근 제어 방식: Users: 개별 사용자
Groups: 여러 사용자를 묶은 논리적 단위

Executives 그룹 → 전체 대시보드 접근
Employees 그룹 → 제한된 대시보드 접근

정답 : B
## Q14(pdf Q#39)
한 회사가 웹사이트에서 검색 가능한 상품 저장소를 운영하고 있습니다. 데이터는 Amazon RDS for MySQL 데이터베이스 테이블에 저장되며,
1천만 개 이상의 행을 포함하고 있습니다. 데이터베이스에는 2TB의 범용 SSD 스토리지가 있습니다. 이 데이터는 매일 수백만 건의 업데이트가 회사 웹사이트를 통해 이루어집니다.
회사는 일부 삽입 작업에 10초 이상 소요되는 것을 발견했습니다. 회사는 데이터베이스 스토리지 성능이 문제라고 판단했습니다.
이 성능 문제를 해결할 수 있는 솔루션은 무엇입니까?

A. 스토리지 유형을 프로비저닝된 IOPS SSD로 변경합니다.
B. DB 인스턴스를 메모리 최적화 인스턴스 클래스로 변경합니다.
C. DB 인스턴스를 버스터블 성능 인스턴스 클래스로 변경합니다.
D. MySQL 네이티브 비동기 복제를 사용하여 다중 AZ RDS 읽기 복제본을 활성화합니다.

General Purpose SSD (gp2 / gp3)

일반적인 워크로드용
IOPS가 스토리지 크기 또는 설정값에 의존
트래픽이 많고 쓰기(INSERT/UPDATE)가 폭증하면 병목 발생 가능

Provisioned IOPS SSD (io1 / io2)

IOPS를 명시적으로 지정
대규모 OLTP, 잦은 INSERT/UPDATE에 최적
지속적이고 예측 가능한 고성능 제공

Provisioned IOPS로 바꾸는 게 정답 

정답 : A
## Q15(pdf Q#86)
한 회사에서 여러 웹 서버가 공통의 Amazon RDS MySQL Multi-AZ DB 인스턴스에 자주 액세스해야 합니다. 이 회사는 웹 서버가 데이터베이스에 안전하게 연결하는 동시에 사용자 자격 증명을 자주 교체해야 하는 보안 요구 사항을 충족하는 방법을 원합니다.
다음 중 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

A. 데이터베이스 사용자 자격 증명을 AWS Secrets Manager에 저장합니다. 웹 서버가 AWS Secrets Manager에 액세스할 수 있도록 필요한 IAM 권한을 부여합니다.
B. 데이터베이스 사용자 자격 증명을 AWS Systems Manager OpsCenter에 저장합니다. 웹 서버가 OpsCenter에 액세스할 수 있도록 필요한 IAM 권한을 부여합니다.
C. 데이터베이스 사용자 자격 증명을 안전한 Amazon S3 버킷에 저장합니다. 웹 서버가 자격 증명을 검색하고 데이터베이스에 액세스할 수 있도록 필요한 IAM 권한을 부여합니다.
D. 데이터베이스 사용자 자격 증명을 웹 서버 시스템의 AWS Key Management Service(AWS KMS)로 암호화된 파일에 저장합니다.
웹 서버는 파일을 복호화하고 데이터베이스에 액세스할 수 있어야 합니다.

AWS Secrets Manager
AWS에서 제공하는 관리형 비밀 관리 서비스

주요 기능

데이터베이스 자격 증명 저장
자동 비밀번호 회전 (Rotation)
RDS(MySQL, PostgreSQL 등)와 네이티브 통합
IAM 정책으로 접근 제어
암호화(KMS) 자동 처리

정답 : A
## Q16(pdf Q#87)
한 회사가 Amazon API Gateway API에서 호출되는 AWS Lambda 함수에서 애플리케이션을 호스팅합니다. Lambda 함수는 고객 데이터를 Amazon Aurora MySQL 데이터베이스에 저장합니다. 회사가 데이터베이스를 업그레이드할 때마다 Lambda 함수는 업그레이드가 완료될 때까지 데이터베이스 연결을 설정하지 못합니다.
그 결과 일부 이벤트에 대한 고객 데이터가 기록되지 않습니다.
솔루션 아키텍트는 데이터베이스 업그레이드 중에 생성되는 고객 데이터를 저장하는 솔루션을 설계해야 합니다.
다음 중 어떤 솔루션이 이러한 요구 사항을 충족할까요?

A. Lambda 함수와 데이터베이스 사이에 Amazon RDS 프록시를 프로비저닝합니다. Lambda 함수가 RDS 프록시에 연결하도록 구성합니다.
B. Lambda 함수의 실행 시간을 최대로 늘립니다. 고객 데이터를 데이터베이스에 저장하는 코드에 재시도 메커니즘을 추가합니다.
C. 고객 데이터를 Lambda 로컬 스토리지에 저장합니다. 새로운 Lambda 함수가 로컬 스토리지를 스캔하여 고객 데이터를 데이터베이스에 저장하도록 구성합니다.
D. 고객 데이터를 Amazon Simple Queue Service(Amazon SQS) FIFO 큐에 저장합니다. 큐를 주기적으로 확인하고 고객 데이터를 데이터베이스에 저장하는 새로운 Lambda 함수를 생성합니다.

SQS = 비동기 버퍼(내구성 있는 임시 저장소)

Lambda가 즉시 DB에 쓰지 못해도
메시지를 안전하게 저장
DB가 복구되면 나중에 다시 처리 가능

왜 FIFO 큐인가?

고객 데이터는:

순서 보장 필요할 가능성 큼
중복 처리 방지 필요

FIFO 큐 특징:

순서 보장
exactly-once 처리

정답 : D
## Q17(pdf Q#90)
한 회사가 공개적으로 접근 가능한 영화 데이터를 저장하기 위해 SQL 데이터베이스를 사용하고 있습니다. 이 데이터베이스는 Amazon RDS Single-AZ DB 인스턴스에서 실행됩니다.
스크립트는 매일 임의의 간격으로 쿼리를 실행하여 데이터베이스에 추가된 새 영화 수를 기록합니다. 이 스크립트는
업무 시간 중에 최종 총계를 보고해야 합니다.
회사의 개발팀은 스크립트가 실행될 때 개발 작업에 필요한 데이터베이스 성능이 부족하다는 것을 발견했습니다.
솔루션 아키텍트는 이 문제를 해결하기 위한 솔루션을 권장해야 합니다.
다음 중 운영 오버헤드가 가장 적은 솔루션은 무엇입니까?

A. DB 인스턴스를 Multi-AZ 배포로 변경합니다.
B. 데이터베이스의 읽기 복제본을 생성하고, 스크립트가 읽기 복제본만 쿼리하도록 구성합니다.
C. 개발팀에게 매일 업무 종료 시 데이터베이스의 항목을 수동으로 내보내도록 지시합니다.
D. 스크립트가 데이터베이스에 대해 실행하는 일반적인 쿼리를 Amazon ElastiCache를 사용하여 캐싱합니다.

정답 : B