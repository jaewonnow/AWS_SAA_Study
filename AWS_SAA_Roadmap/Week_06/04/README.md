# Placeholder
## Q1(pdf Q#140)
솔루션 아키텍트는 한 회사가 AWS에서 애플리케이션을 실행하는 비용을 최적화하도록 지원해야 합니다. 이 애플리케이션은 아키텍처 내에서 컴퓨팅을 위해 Amazon EC2 인스턴스, AWS Fargate 및 AWS Lambda를 사용합니다.
EC2 인스턴스는 애플리케이션의 데이터 수집 계층을 실행합니다. EC2 사용량은 불규칙적이고 예측하기 어렵습니다. EC2 인스턴스에서 실행되는 워크로드는 언제든지 중단될 수 있습니다.
애플리케이션 프런트엔드는 Fargate에서 실행되고 Lambda는 API 계층을 제공합니다. 프런트엔드 및 API 계층의 사용률은 향후 1년 동안 예측 가능합니다.
다음 중 어떤 구매 옵션 조합이 이 애플리케이션을 호스팅하는 데 가장 비용 효율적인 솔루션을 제공할까요? (두 가지를 선택하세요.)

A. 데이터 수집 계층에 스팟 인스턴스 사용
B. 데이터 수집 계층에 온디맨드 인스턴스 사용
C. 프런트엔드 및 API 계층에 1년 컴퓨팅 절약 플랜 구매
D. 데이터 수집 계층에 1년 선불 예약 인스턴스 구매
E. 프런트엔드 및 API 계층을 위해 1년 EC2 인스턴스 절약 플랜을 구매하세요.

Spot Instances
남는 EC2 용량을 저렴하게 사용 
최대 90% 비용 절감 
AWS가 회수할 수 있음 (2분 알림)

Compute Savings Plan
EC2, Fargate, Lambda 모두 적용 가능 
특정 인스턴스 타입/리전 고정 X 
시간당 컴퓨팅 사용량(commitment) 기반 할인

정답 : A , C

## Q2(pdf Q#408)
한 회사가 UDP를 사용하는 지리적으로 분산된 수천 개의 원격 장치에서 데이터를 수신하는 애플리케이션을 운영하고 있습니다. 이 애플리케이션은
데이터를 즉시 처리하고 필요한 경우 장치로 메시지를 다시 보냅니다. 데이터는 저장되지 않습니다.
이 회사는 장치에서 장치로의 데이터 전송 지연 시간을 최소화하는 솔루션이 필요합니다. 또한 이 솔루션은 다른 AWS 리전으로의 빠른 장애 조치를 제공해야 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

A. Amazon Route 53 장애 조치 라우팅 정책을 구성합니다. 두 리전 각각에 네트워크 로드 밸런서(NLB)를 생성합니다. NLB가 AWS Lambda 함수를 호출하여 데이터를 처리하도록 구성합니다. 
B. AWS Global Accelerator를 사용합니다. 두 리전 각각에 엔드포인트로 네트워크 로드 밸런서(NLB)를 생성합니다. Fargate 시작 유형으로 Amazon Elastic Container Service(Amazon ECS) 클러스터를 생성합니다. 클러스터에 ECS 서비스를 생성합니다. ECS 서비스를 NLB의 대상으로 설정하고 Amazon ECS에서 데이터를 처리합니다. 
C. AWS Global Accelerator를 사용합니다. 두 리전 각각에 엔드포인트로 애플리케이션 로드 밸런서(ALB)를 생성합니다. Fargate 시작 유형으로 Amazon Elastic Container Service(Amazon ECS) 클러스터를 생성합니다. 클러스터에 ECS 서비스를 생성합니다. ECS 서비스를 ALB의 대상으로 설정하고 Amazon ECS에서 데이터를 처리합니다. 
D. Amazon Route 53 장애 조치 라우팅 정책을 구성합니다. 두 리전 각각에 애플리케이션 로드 밸런서(ALB)를 생성합니다. Fargate 시작 유형을 사용하여 Amazon Elastic Container Service(Amazon ECS) 클러스터를 생성합니다. 클러스터에 ECS 서비스를 생성합니다. ECS 서비스를 ALB의 대상으로 설정합니다. Amazon ECS에서 데이터를 처리합니다.

AWS Global Accelerator

Anycast IP 제공
사용자 → 가장 가까운 AWS Edge 로 유입
AWS 글로벌 백본 네트워크 사용
DNS보다 훨씬 빠른 장애 조치 (초 단위)

Remote Devices (UDP)
   ↓
AWS Global Accelerator (Anycast IP)
   ↓
NLB (Region A / Region B)
   ↓
ECS Fargate Service
-> 최소 지연, 글로벌 사용자 최적 경로, 리전 장애시 즉시 전환

정답 : B
## Q3(pdf Q#483)
한 회사가 .NET 6 Framework에서 실행되는 Windows 작업을 Windows 컨테이너로 컨테이너화했습니다. 이 회사는 이 작업을 AWS 클라우드에서 실행하려고 합니다.
작업은 10분마다 실행되며, 실행 시간은 1분에서 3분 사이입니다.
다음 중 어떤 솔루션이 이러한 요구 사항을 가장 비용 효율적으로 충족할까요?

A. 작업의 컨테이너 이미지를 기반으로 AWS Lambda 함수를 생성합니다. Amazon EventBridge를 구성하여 10분마다 함수를 호출합니다.
B. AWS Batch를 사용하여 AWS Fargate 리소스를 사용하는 작업을 생성합니다. 작업 일정을 10분마다 실행되도록 구성합니다.
C. AWS Fargate에서 Amazon Elastic Container Service(Amazon ECS)를 사용하여 작업을 실행합니다. 작업의 컨테이너 이미지를 기반으로 10분마다 실행되는 예약된 작업을 생성합니다.
D. AWS Fargate에서 Amazon Elastic Container Service(Amazon ECS)를 사용하여 작업을 실행합니다. 작업의 컨테이너 이미지를 기반으로 독립 실행형 작업을 생성합니다.
Windows 작업 스케줄러를 사용하여 10분마다 작업을 실행하세요.

ECS Fargate Scheduled Task

ECS에서 컨테이너를 일정 주기로 실행
실행될 때만 리소스 사용
실행 종료 시 비용 과금 중단
서버 관리 X

정답 : C
## Q4(pdf Q#486)
한 회사가 AWS에서 3계층 애플리케이션을 구축하고 있습니다. 프레젠테이션 계층은 정적 웹사이트를 제공하고, 로직 계층은 컨테이너화된 애플리케이션입니다.
이 애플리케이션은 관계형 데이터베이스에 데이터를 저장합니다. 회사는 배포를 간소화하고 운영 비용을 절감하고자 합니다.
다음 중 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

A. Amazon S3를 사용하여 정적 콘텐츠를 호스팅합니다. Amazon Elastic Container Service(Amazon ECS)와 AWS Fargate를 사용하여 컴퓨팅 성능을 확보합니다.
데이터베이스에는 관리형 Amazon RDS 클러스터를 사용합니다.
B. Amazon CloudFront를 사용하여 정적 콘텐츠를 호스팅합니다. Amazon Elastic Container Service(Amazon ECS)와 Amazon EC2를 사용하여 컴퓨팅 성능을 확보합니다.
데이터베이스에는 관리형 Amazon RDS 클러스터를 사용합니다.
C. Amazon S3를 사용하여 정적 콘텐츠를 호스팅합니다. Amazon Elastic Kubernetes Service(Amazon EKS)와 AWS Fargate를 사용하여 컴퓨팅 성능을 확보합니다.
데이터베이스에는 관리형 Amazon RDS 클러스터를 사용합니다.
D. Amazon EC2 예약 인스턴스를 사용하여 정적 콘텐츠를 호스팅합니다. Amazon Elastic Kubernetes Service(Amazon EKS)와 Amazon EC2를 사용하여 컴퓨팅 성능을 확보합니다.
데이터베이스에는 관리형 Amazon RDS 클러스터를 사용하십시오.

Presentation Tier → Amazon S3
정적 웹사이트 호스팅에 최적
서버 없음
매우 저렴
고가용성 기본 제공

Data Tier → Amazon RDS
백업, 패치, 장애 조치 자동
관계형 DB 요구 충족
운영 부담 최소

정답 : A

## Q5(pdf Q#52)
한 회사가 온프레미스 애플리케이션을 AWS로 마이그레이션하려고 합니다. 이 애플리케이션은 수십 기가바이트에서 수백 테라바이트에 이르는 다양한 크기의 출력 파일을 생성합니다.
애플리케이션 데이터는 표준 파일 시스템 구조에 저장되어야 합니다. 회사는 자동 확장이 가능하고, 고가용성을 제공하며, 운영 오버헤드가 최소화된 솔루션을 원합니다.
다음과 같은 요구 사항을 충족하는 솔루션은 무엇일까요?

A. 애플리케이션을 Amazon Elastic Container Service(Amazon ECS)에서 컨테이너로 실행되도록 마이그레이션합니다. 스토리지로는 Amazon S3를 사용합니다.
B. 애플리케이션을 Amazon Elastic Kubernetes Service(Amazon EKS)에서 컨테이너로 실행되도록 마이그레이션합니다. 스토리지로는 Amazon Elastic Block Store(Amazon EBS)를 사용합니다.
C. 애플리케이션을 다중 가용 영역(Multi-AZ) 자동 스케일링 그룹의 Amazon EC2 인스턴스로 마이그레이션합니다. 스토리지로는 Amazon Elastic File System(Amazon EFS)을 사용합니다.
D. 애플리케이션을 다중 가용 영역(Multi-AZ) 자동 스케일링 그룹의 Amazon EC2 인스턴스로 마이그레이션합니다. 스토리지로는 Amazon Elastic Block Store(Amazon EBS)를 사용하세요.

EFS
완전 관리형 NFS 파일 시스템
여러 EC2 인스턴스에서 동시에 마운트 가능
자동 용량 확장 (GB → PB 단위)
Multi-AZ 기본 지원
서버/스토리지 관리 X

EC2 Auto Scaling Group (Multi-AZ)
          ↓
     Amazon EFS
 (Auto-scale, HA, File System)


정답 : C

## Q6(pdf Q#58)
한 회사가 확장성과 가용성 요구 사항을 충족하기 위해 핵심 애플리케이션을 컨테이너에서 실행하려고 합니다. 이 회사는 핵심 애플리케이션 유지 관리에 집중하기를 원하며, 컨테이너화된 워크로드를 실행하는 데 필요한 기본 인프라의 프로비저닝 및 관리는 담당하고 싶지 않습니다.

솔루션 아키텍트는 이러한 요구 사항을 충족하기 위해 무엇을 해야 할까요?

A. Amazon EC2 인스턴스를 사용하고 해당 인스턴스에 Docker를 설치합니다.
B. Amazon EC2 워커 노드에서 Amazon Elastic Container Service(Amazon ECS)를 사용합니다.
C. AWS Fargate에서 Amazon Elastic Container Service(Amazon ECS)를 사용합니다.
D. Amazon Elastic Container Service(Amazon ECS)에 최적화된 Amazon Machine Image(AMI)에서 Amazon EC2 인스턴스를 사용합니다.

AWS Fargate

Fargate = 서버리스 컨테이너 실행 엔진
EC2 인스턴스 프로비저닝 X
패치 / AMI / 용량 관리 X
컨테이너 단위로 실행 & 과금
ECS와 완전 통합

ECS on Fargate의 장점

고가용성 기본 제공
자동 확장
운영 오버헤드 최소
AWS가 인프라 전부 관리

정답 : C

## Q7(pdf Q#112)
한 회사가 온프레미스 서버 세트에 컨테이너화된 웹 애플리케이션을 호스팅하고 있으며, 이 서버들은 들어오는 요청을 처리합니다. 요청 수가 빠르게 증가하고 있습니다. 온프레미스 서버는 늘어난 요청을 처리할 수 없습니다. 회사는 최소한의 코드 변경과 개발 노력으로 애플리케이션을 AWS로 이전하려고 합니다.
다음 중 운영 오버헤드가 가장 적은 솔루션은 무엇일까요?

A. Amazon Elastic Container Service(Amazon ECS)에서 AWS Fargate를 사용하여 서비스 자동 스케일링을 통해 컨테이너화된 웹 애플리케이션을 실행합니다.
Application Load Balancer를 사용하여 들어오는 요청을 분산합니다.
B. 두 개의 Amazon EC2 인스턴스를 사용하여 컨테이너화된 웹 애플리케이션을 호스팅합니다. Application Load Balancer를 사용하여 들어오는 요청을 분산합니다.
C. 지원되는 언어 중 하나를 사용하는 새로운 코드로 AWS Lambda를 사용합니다. 부하를 처리하기 위해 여러 개의 Lambda 함수를 생성합니다.
Amazon API Gateway를 Lambda 함수의 진입점으로 사용합니다.
D. AWS ParallelCluster와 같은 고성능 컴퓨팅(HPC) 솔루션을 사용하여 들어오는 요청을 적절한 규모로 처리할 수 있는 HPC 클러스터를 구축합니다.

ECS + Fargate

기존 컨테이너 이미지 그대로 사용 가능
EC2 서버 관리 X
OS 패치 X
용량 계획 X

Service Auto Scaling

요청 수 증가 시: 컨테이너 자동 증가
트래픽 감소 시: 자동 축소

정답 : A

## Q8(pdf Q#128)
한 회사가 AWS 클라우드에서 컨테이너 기반 애플리케이션을 실행하려고 합니다. 이러한 애플리케이션은 상태를 저장하지 않으며, 기본 인프라의 장애를 허용할 수 있습니다.
이 회사는 비용과 운영 오버헤드를 최소화하는 솔루션을 필요로 합니다.
이러한 요구 사항을 충족하기 위해 솔루션 아키텍트는 무엇을 해야 할까요?

A. Amazon EC2 Auto Scaling 그룹의 스팟 인스턴스를 사용하여 애플리케이션 컨테이너를 실행합니다.
B. Amazon Elastic Kubernetes Service(Amazon EKS) 관리형 노드 그룹의 스팟 인스턴스를 사용합니다.
C. Amazon EC2 Auto Scaling 그룹의 온디맨드 인스턴스를 사용하여 애플리케이션 컨테이너를 실행합니다.
D. Amazon Elastic Kubernetes Service(Amazon EKS) 관리형 노드 그룹의 온디맨드 인스턴스를 사용합니다.

Spot Instances

AWS의 남는 EC2 용량 사용
최대 90% 비용 절감
언제든지 회수 가능

Amazon EKS Managed Node Group

EC2 노드 프로비저닝 자동
노드 교체 / 헬스 관리
Auto Scaling 통합
Kubernetes 제어 플레인 완전 관리형

정답 : B

## Q9(pdf Q#163)
한 회사가 온프레미스에서 컨테이너화된 애플리케이션을 구축하다가 AWS로 이전하기로 결정했습니다. 이 애플리케이션은 배포 직후 수천 명의 사용자를 확보할 것으로 예상됩니다. 회사는 대규모 컨테이너 배포를 어떻게 관리해야 할지 확신하지 못하고 있습니다. 또한, 운영 오버헤드를 최소화하면서 고가용성 아키텍처로 컨테이너화된 애플리케이션을 배포해야 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

A. 컨테이너 이미지를 Amazon Elastic Container Registry(Amazon ECR) 리포지토리에 저장합니다. AWS Fargate 시작 유형을 사용하는 Amazon Elastic Container Service(Amazon ECS) 클러스터를 사용하여 컨테이너를 실행합니다. 대상 추적을 사용하여 수요에 따라 자동으로 확장합니다.
B. 컨테이너 이미지를 Amazon Elastic Container Registry(Amazon ECR) 리포지토리에 저장합니다. Amazon EC2 시작 유형을 사용하는 Amazon Elastic Container Service(Amazon ECS) 클러스터를 사용하여 컨테이너를 실행합니다. 대상 추적을 사용하여 수요에 따라 자동으로 확장합니다.
C. 컨테이너 이미지를 Amazon EC2 인스턴스에서 실행되는 리포지토리에 저장합니다. 여러 가용 영역에 분산된 EC2 인스턴스에서 컨테이너를 실행합니다. Amazon CloudWatch에서 평균 CPU 사용률을 모니터링합니다. 필요에 따라 새 EC2 인스턴스를 시작합니다.
D. 컨테이너 이미지가 포함된 Amazon EC2 Amazon Machine Image(AMI)를 생성합니다. 여러 가용 영역에 걸쳐 Auto Scaling 그룹에서 EC2 인스턴스를 시작합니다. 평균 CPU 사용률 임계값이 초과되면 Amazon CloudWatch 알람을 사용하여 EC2 인스턴스를 확장합니다.

Amazon ECR
AWS 완전관리형 컨테이너 레지스트리
IAM 통합, 보안, 확장성 기본 제공
ECS/Fargate와 네이티브 통합

ECS with Fargate란?

서버를 전혀 관리하지 않는 컨테이너 실행 방식

EC2 인스턴스 X
Auto Scaling 그룹 X
패치, 용량, 노드 장애 X

정답 : A

## Q10(pdf Q#185)
한 회사가 Amazon ECS를 사용하여 애플리케이션을 실행합니다. 이 애플리케이션은 원본 이미지의 크기를 조정한 버전을 생성한 다음 Amazon S3 API를 호출하여 크기가 조정된 이미지를 Amazon S3에 저장합니다.
솔루션 아키텍트는 애플리케이션이 Amazon S3에 액세스할 수 있는 권한을 확보하려면 어떻게 해야 할까요?

A. AWS IAM에서 S3 역할을 업데이트하여 Amazon ECS에서 읽기/쓰기 액세스를 허용한 다음 컨테이너를 다시 시작합니다.
B. S3 권한이 있는 IAM 역할을 생성하고 해당 역할을 작업 정의의 taskRoleArn으로 지정합니다.
C. Amazon ECS에서 Amazon S3에 대한 액세스를 허용하는 보안 그룹을 생성하고 ECS 클러스터에서 사용하는 시작 구성을 업데이트합니다.
D. S3 권한이 있는 IAM 사용자를 생성한 다음 해당 계정으로 로그인하여 ECS 클러스터용 Amazon EC2 인스턴스를 다시 시작합니다.

ECS의 IAM 역할

역할	                     용도
Task execution role	        ECR에서 이미지 pull, CloudWatch 로그 전송
Task role (taskRoleArn)	    컨테이너 애플리케이션이 AWS API 호출

taskRoleArn

ECS Task Definition에 설정
컨테이너 내부 애플리케이션이:
aws-sdk
aws cli
S3 API
를 호출할 때 자동으로 사용됨

정답 : B

## Q11(pdf Q#187)
한 회사가 로드 밸런싱 프런트엔드, 컨테이너 기반 애플리케이션, 관계형 데이터베이스로 구성된 전자상거래 애플리케이션을 개발 중입니다.
솔루션 아키텍트는 수동 개입을 최소화하면서 고가용성을 갖춘 솔루션을 구축해야 합니다.
다음 중 이러한 요구 사항을 충족하는 솔루션은 무엇입니까? (두 가지를 선택하십시오.)

A. Multi-AZ 모드로 Amazon RDS DB 인스턴스를 생성합니다.
B. 다른 가용 영역에 Amazon RDS DB 인스턴스와 하나 이상의 복제본을 생성합니다.
C. 동적 애플리케이션 로드를 처리하기 위해 Amazon EC2 인스턴스 기반 Docker 클러스터를 생성합니다.
D. 동적 애플리케이션 로드를 처리하기 위해 Fargate 시작 유형의 Amazon Elastic Container Service(Amazon ECS) 클러스터를 생성합니다.
E. 동적 애플리케이션 로드를 처리하기 위해 Amazon EC2 시작 유형의 Amazon Elastic Container Service(Amazon ECS) 클러스터를 생성합니다.

Amazon RDS Multi-AZ
주 DB + 대기(standby) DB를 다른 AZ에 자동 생성
동기식 복제
장애 발생 시:
    자동 Failover
    애플리케이션 변경 거의 없음

ECS + Fargate

서버리스 컨테이너 실행
EC2 인스턴스:
생성 X
패치 X
스케일링 X
컨테이너만 정의하면 끝

정답 : A,D

## Q12(pdf Q#198)
한 회사가 온프레미스 데이터 센터의 Kubernetes 클러스터에서 컨테이너화된 애플리케이션을 실행하고 있습니다. 데이터 저장을 위해 MongoDB 데이터베이스를 사용하고 있습니다.
이 회사는 이러한 환경 중 일부를 AWS로 마이그레이션하려고 하지만, 현재로서는 코드 변경이나 배포 방식 변경이 불가능합니다.
운영 오버헤드를 최소화하는 솔루션이 필요합니다.
다음 중 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

A. 컴퓨팅에는 Amazon EC2 워커 노드를 사용하는 Amazon Elastic Container Service(Amazon ECS)와 데이터 저장에는 EC2의 MongoDB를 사용합니다.
B. 컴퓨팅에는 AWS Fargate를 사용하는 Amazon Elastic Container Service(Amazon ECS)와 데이터 저장에는 Amazon DynamoDB를 사용합니다.
C. 컴퓨팅에는 Amazon EC2 워커 노드를 사용하는 Amazon Elastic Kubernetes Service(Amazon EKS)와 데이터 저장에는 Amazon DynamoDB를 사용합니다.
D. 컴퓨팅에는 AWS Fargate를 사용하는 Amazon Elastic Kubernetes Service(Amazon EKS)와 데이터 저장에는 Amazon DocumentDB(MongoDB 호환성 포함)를 사용합니다.

정답 : D

## Q13(pdf Q#220)
솔루션 아키텍트가 사용자의 요청을 수신하는 새로운 API를 Amazon API Gateway를 사용하여 설계하고 있습니다. 요청량은 매우 가변적이며, 몇 시간 동안 요청이 전혀 없을 수도 있습니다. 데이터 처리는 비동기적으로 이루어지지만, 요청이 들어온 후 몇 초 이내에 완료되어야 합니다.
솔루션 아키텍트는 요구 사항을 가장 낮은 비용으로 충족하기 위해 어떤 컴퓨팅 서비스를 API에서 호출해야 할까요?

A. AWS Glue 작업
B. AWS Lambda 함수
C. Amazon Elastic Kubernetes Service(Amazon EKS)에서 호스팅되는 컨테이너화된 서비스
D. Amazon EC2를 사용하여 Amazon ECS에서 호스팅되는 컨테이너화된 서비스

AWS Lambda

요청이 있을 때만 실행
실행 시간(ms 단위) + 호출 횟수로 과금
유휴 비용 = 0

정답 : B

## Q14(pdf Q#223)
한 회사가 Amazon Elastic Kubernetes Service(Amazon EKS)의 프라이빗 서브넷에서 실행되는 Pod로 Java Spring Boot 애플리케이션을 배포했습니다.
이 애플리케이션은 Amazon DynamoDB 테이블에 데이터를 기록해야 합니다. 솔루션 아키텍트는 애플리케이션이 인터넷에 트래픽을 노출하지 않고 DynamoDB 테이블과 상호 작용할 수 있도록 해야 합니다.
이 목표를 달성하기 위해 솔루션 아키텍트가 취해야 할 단계 조합은 무엇입니까? (두 가지를 선택하십시오.)

A. EKS Pod에 충분한 권한을 가진 IAM 역할을 연결합니다.
B. EKS Pod에 충분한 권한을 가진 IAM 사용자를 연결합니다.
C. 프라이빗 서브넷의 네트워크 ACL을 통해 DynamoDB 테이블에 대한 아웃바운드 연결을 허용합니다.
D. DynamoDB용 VPC 엔드포인트를 생성합니다.
E. Java Spring Boot 코드에 액세스 키를 포함합니다.

IAM Role
AWS 서비스 접근은 IAM Role이 표준
Access Key를 코드에 넣지 않음
자동 키 로테이션
최소 권한 원칙 적용 가능

DynamoDB용 VPC Endpoint
DynamoDB는 기본적으로 퍼블릭 엔드포인트
Private Subnet에서 접근하려면:
NAT Gateway X (인터넷 경유)
VPC Endpoint O

정답 : A,D