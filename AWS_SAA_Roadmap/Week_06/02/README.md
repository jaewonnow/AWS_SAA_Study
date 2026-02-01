# Week06 - ECS , Fargate , ECR , EKS

## Q140

### 🧩 문제 요약

컴퓨팅이 EC2(데이터 인제스트, 사용량 불규칙/중단 가능), Fargate(프런트엔드, 1년간 사용량 예측 가능), Lambda(API, 1년간 예측 가능)로 구성된다. 가장 비용 효율적인 구매 옵션을 2개 선택해야 한다.

### ✅ 정답

**A. Use Spot Instances for the data ingestion layer**
**C. Purchase a 1-year Compute Savings Plan for the front end and API layer.**

### 🔍 정리

- 데이터 인제스트(EC2)는 Spot Instances → 사용량이 불규칙하고 중단 허용이므로 가장 큰 비용 절감 효과

- 프런트엔드(Fargate) + API(Lambda)는 1-year Compute Savings Plan → EC2뿐 아니라 Fargate/Lambda까지 커버하면서 예측 가능한 사용량에 대한 장기 할인 적용

## Q408

### 🧩 문제 요약

전 세계에 분산된 수천 대 UDP 디바이스가 데이터를 보내고, 앱이 즉시 처리 후 응답한다(저장 없음). 목표는 전송 지연 최소화(글로벌 저지연) + 다른 리전으로 빠른 장애조치다.

### ✅ 정답

**B. Use AWS Global Accelerator. Create a Network Load Balancer (NLB) in each of the two Regions as an endpoint. Create an Amazon Elastic Container Service (Amazon ECS) cluster with the Fargate launch type. Create an ECS service on the cluster. Set the ECS service as the target for the NLB. Process the data in Amazon ECS.**

### 🔍 정리

- 글로벌 엔트리 포인트는 AWS Global Accelerator → 사용자(디바이스)와 가장 가까운 엣지로 유입시켜 UDP 전송 지연 최소화 + 헬스체크 기반 리전 간 빠른 페일오버

- 로드밸런서는 NLB → UDP 지원(ALB는 UDP 미지원) + 초저지연 L4 처리에 적합

- 처리 계층은 ECS Fargate → 서버 관리 없이 확장/운영 가능, “즉시 처리 후 응답” 워크로드에 맞게 운영 오버헤드 최소

## Q483

Windows 컨테이너(.NET 6)로 패키징된 잡을 AWS에서 실행해야 하며 10분마다 실행되고 1~3분만 짧게 동작한다. 목표는 가장 비용 효율적인 운영 방식이다.

### ✅ 정답

**C. Use Amazon Elastic Container Service (Amazon ECS) on AWS Fargate to run the job. Create a scheduled task based on the container image of the job to run every 10 minutes.**

### 🔍 정리

- 실행 방식은 ECS Fargate Scheduled Task → 10분마다 필요한 동안만 컨테이너가 떠서 실행되고 종료되므로 유휴 비용 없이 pay-per-use로 가장 경제적

- 워크로드가 Windows 컨테이너이므로 Fargate에서 Windows 태스크를 실행하는 구성이 요구사항에 부합

## Q486

3-티어 앱에서 프레젠테이션은 정적 웹사이트, 로직은 컨테이너, 데이터는 관계형 DB를 사용한다. 목표는 배포 단순화와 운영비 절감(운영 오버헤드 최소화)이다.

### ✅ 정답

**A. Use Amazon S3 to host static content. Use Amazon Elastic Container Service (Amazon ECS) with AWS Fargate for compute power. Use a managed Amazon RDS cluster for the database.**

### 🔍 정리

- 프런트(정적 사이트)는 S3 정적 호스팅 → 서버 운영 없이 비용 최소 + 배포 단순

- 로직(컨테이너)은 ECS Fargate → EC2 노드 관리/패치/용량 계획 없이 실행, 자동 확장으로 운영비·운영 부담 최소

- DB는 관리형 RDS 클러스터 → 백업/패치/HA 자동화로 직접 운영 대비 비용·운영 오버헤드 최소

### 회고

일단 기본 개념 정리가 완벽하지 않아서 필수 문제만 풀고 추가로 공부 후 문제 더 풀어보겠습니다.
