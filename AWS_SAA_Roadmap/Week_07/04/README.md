# Placeholder
## Q1(pdf Q#12)
한 글로벌 기업이 애플리케이션 로드 밸런서(ALB) 뒤의 Amazon EC2 인스턴스에 웹 애플리케이션을 호스팅하고 있습니다. 웹 애플리케이션에는 정적 데이터와 동적 데이터가 포함되어 있습니다. 이 회사는 정적 데이터를 Amazon S3 버킷에 저장합니다. 이 회사는 정적 데이터와 동적 데이터의 성능을 향상시키고 지연 시간을 줄이고자 합니다. 또한 Amazon Route 53에 등록된 자체 도메인 이름을 사용하고 있습니다.
솔루션 아키텍트는 이러한 요구 사항을 충족하기 위해 무엇을 해야 할까요?

A. S3 버킷과 ALB를 오리진으로 하는 Amazon CloudFront 배포를 생성합니다. Route 53을 구성하여 트래픽을 CloudFront 배포로 라우팅합니다.
B. ALB를 오리진으로 하는 Amazon CloudFront 배포를 생성합니다. S3 버킷을 엔드포인트로 하는 AWS Global Accelerator 표준 가속기를 생성합니다. Route 53을 구성하여 트래픽을 CloudFront 배포로 라우팅합니다.
C. S3 버킷을 오리진으로 하는 Amazon CloudFront 배포를 생성합니다. ALB와 CloudFront 배포를 엔드포인트로 하는 AWS Global Accelerator 표준 가속기를 생성합니다. 가속기 DNS 이름을 가리키는 사용자 지정 도메인 이름을 생성합니다. 웹 애플리케이션의 엔드포인트로 사용자 지정 도메인 이름을 사용합니다.
D. ALB를 오리진으로 하는 Amazon CloudFront 배포를 생성합니다. S3 버킷을 엔드포인트로 하는 AWS Global Accelerator 표준 가속기를 생성합니다. 두 개의 도메인 이름을 생성합니다. 하나의 도메인 이름은 동적 콘텐츠용 CloudFront DNS 이름으로 연결하고, 다른 도메인 이름은 정적 콘텐츠용 액셀러레이터 DNS 이름으로 연결합니다. 이러한 도메인 이름을 웹 애플리케이션의 엔드포인트로 사용합니다.

CloudFront
전 세계 Edge Location 캐싱
정적 파일: 캐싱
동적 요청: 가장 가까운 엣지 → ALB로 전달
TLS/연결 최적화
지연시간 감소

정답 : A

## Q2(pdf Q#29)
한 회사가 UDP 연결을 사용하는 VoIP(Voice over Internet Protocol) 서비스를 제공합니다. 이 서비스는 Auto Scaling 그룹에서 실행되는 Amazon EC2 인스턴스로 구성됩니다. 회사는 여러 AWS 리전에 서비스를 배포했습니다.
이 회사는 사용자를 지연 시간이 가장 짧은 리전으로 연결해야 합니다. 또한 리전 간 자동 장애 조치 기능도 필요합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

A. 네트워크 로드 밸런서(NLB)와 연결된 대상 그룹을 배포합니다. 대상 그룹을 Auto Scaling 그룹과 연결합니다.
각 리전에서 NLB를 AWS Global Accelerator 엔드포인트로 사용합니다.
B. 애플리케이션 로드 밸런서(ALB)와 연결된 대상 그룹을 배포합니다. 대상 그룹을 Auto Scaling 그룹과 연결합니다.
각 리전에서 ALB를 AWS Global Accelerator 엔드포인트로 사용합니다.
C. 네트워크 로드 밸런서(NLB)와 연결된 대상 그룹을 배포합니다. 대상 그룹을 Auto Scaling 그룹과 연결합니다.
각 NLB의 별칭을 가리키는 Amazon Route 53 지연 시간 레코드를 생성합니다.
이 지연 시간 레코드를 오리진으로 사용하는 Amazon CloudFront 배포를 생성합니다.
D. 애플리케이션 로드 밸런서(ALB)와 연결된 대상 그룹을 배포합니다. 대상 그룹을 Auto Scaling 그룹과 연결합니다.
각 ALB의 별칭을 가리키는 Amazon Route 53 가중치 레코드를 생성합니다. 가중치가 적용된 레코드를 오리진으로 사용하는 Amazon CloudFront 배포를 배포합니다.

User
 ↓
Global Accelerator
 ↓
각 리전 NLB
 ↓
EC2 Auto Scaling

장점

UDP 지원 (NLB)
글로벌 라우팅 (GA)
자동 failover
최저 latency
Anycast IP
DNS 캐시 영향 없음

정답 : A

## Q3(pdf Q#38)
한 회사가 Amazon S3에 정적 웹사이트를 호스팅하고 있으며, DNS로 Amazon Route 53을 사용하고 있습니다. 이 웹사이트는 전 세계에서 접속량이 증가하고 있습니다. 회사는 웹사이트에 접속하는 사용자의 지연 시간을 줄여야 합니다.
다음 중 이러한 요구 사항을 가장 비용 효율적으로 충족하는 솔루션은 무엇입니까?

A. 웹사이트가 포함된 S3 버킷을 모든 AWS 리전에 복제합니다. Route 53 지리적 위치 라우팅 항목을 추가합니다.
B. AWS 글로벌 가속기에서 가속기를 프로비저닝합니다. 제공된 IP 주소를 S3 버킷과 연결합니다. Route 53 항목을 수정하여
가속기의 IP 주소를 가리키도록 합니다.
C. S3 버킷 앞에 Amazon CloudFront 배포를 추가합니다. Route 53 항목을 수정하여 CloudFront 배포를 가리키도록 합니다.
D. 버킷에서 S3 전송 가속을 활성화합니다. Route 53 항목을 수정하여 새 엔드포인트를 가리키도록 합니다.

CloudFront = 글로벌 CDN

사용자 → 가까운 CloudFront 엣지 → S3

장점

지연시간 크게 감소
글로벌 성능 개선
비용 효율적 (S3 복제보다 훨씬 저렴)

Route 53에서는:
→ CloudFront distribution으로 DNS만 연결하면 끝

정답 : C

## Q4(pdf Q#56)
한 회사가 아마존 Route 53에 도메인 이름을 등록했습니다. 이 회사는 ca-central-1 리전에 있는 아마존 API 게이트웨이를 백엔드 마이크로서비스 API의 공개 인터페이스로 사용하고 있습니다.
타사 서비스는 이 API를 안전하게 사용합니다. 이 회사는 타사 서비스에서 HTTPS를 사용할 수 있도록 자사 도메인 이름과 해당 인증서를 사용하여 API 게이트웨이 URL을 설계하고자 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

A. API Gateway에서 Name="Endpoint-URL" 및 Value="Company Domain Name"으로 스테이지 변수를 생성하여 기본 URL을 덮어씁니다.
회사 도메인 이름과 연결된 공개 인증서를 AWS Certificate Manager(ACM)로 가져옵니다.
B. 회사 도메인 이름으로 Route 53 DNS 레코드를 생성합니다. 별칭 레코드를 리전 API Gateway 스테이지 엔드포인트로 지정합니다.
회사 도메인 이름과 연결된 공개 인증서를 us-east-1 리전의 AWS Certificate Manager(ACM)로 가져옵니다.
C. 리전 API Gateway 엔드포인트를 생성합니다. API Gateway 엔드포인트를 회사 도메인 이름과 연결합니다.
동일한 리전의 AWS Certificate Manager(ACM)로 회사 도메인 이름과 연결된 공개 인증서를 가져옵니다. 인증서를 API Gateway 엔드포인트에 연결합니다. Route 53을 구성하여 트래픽을 API Gateway 엔드포인트로 라우팅합니다.
D. 리전 API Gateway 엔드포인트를 생성합니다. API Gateway 엔드포인트를 회사 도메인 이름과 연결합니다. 회사 도메인 이름과 연결된 공개 인증서를 us-east-1 리전의 AWS Certificate Manager(ACM)로 가져옵니다. 해당 인증서를 API Gateway API에 연결합니다. 회사 도메인 이름을 사용하여 Route 53 DNS 레코드를 생성합니다. A 레코드를 회사 도메인 이름으로 지정합니다.

Regional API Gateway면
ACM 인증서는 같은 리전에 있어야 함

순서
1.ACM 인증서 (ca-central-1)
2.API Gateway custom domain 생성
3.인증서 연결
4.Route53 → API Gateway alias

정답 : C

## Q5(pdf Q#120)
한 회사가 us-west-2 리전의 네트워크 로드 밸런서(NLB) 뒤에 있는 세 개의 Amazon EC2 인스턴스에 자체 관리형 DNS 솔루션을 구현했습니다.
이 회사의 사용자 대부분은 미국과 유럽에 있습니다. 회사는 솔루션의 성능과 가용성을 개선하고자 합니다.
이를 위해 회사는 eu-west-1 리전에 세 개의 EC2 인스턴스를 생성 및 구성하고, 이 EC2 인스턴스를 새로운 NLB의 대상으로 추가합니다.
이 회사는 어떤 솔루션을 사용하여 모든 EC2 인스턴스로 트래픽을 라우팅할 수 있을까요?

A. 두 개의 NLB 중 하나로 요청을 라우팅하는 Amazon Route 53 지리적 위치 라우팅 정책을 생성합니다. Amazon CloudFront 배포를 생성합니다.
Route 53 레코드를 배포의 오리진으로 사용합니다.
B. AWS Global Accelerator에서 표준 액셀러레이터를 생성합니다. us-west-2 및 eu-west-1에 엔드포인트 그룹을 생성합니다. 두 개의 NLB를 엔드포인트 그룹의 엔드포인트로 추가합니다.
C. 6개의 EC2 인스턴스에 탄력적 IP 주소를 할당합니다. 6개의 EC2 인스턴스 중 하나로 요청을 라우팅하는 Amazon Route 53 지리적 위치 라우팅 정책을 생성합니다. Amazon CloudFront 배포를 생성합니다. Route 53 레코드를 배포의 오리진으로 사용합니다.
D. 두 개의 NLB를 두 개의 ALB(Application Load Balancer)로 교체합니다. 두 개의 ALB 중 하나로 요청을 라우팅하는 Amazon Route 53 지연 시간 라우팅 정책을 생성합니다. Amazon CloudFront 배포를 생성합니다. Route 53 레코드를 배포의 오리진으로 사용합니다.

Global Accelerator

Global Accelerator 생성
Endpoint group:
    us-west-2 NLB
    eu-west-1 NLB
각 리전 NLB endpoint 등록

Global Accelerator는:
사용자 → 가장 가까운 AWS edge → 최적 리전
즉
미국 → us-west-2
유럽 → eu-west-1
자동 연결됨

정답 : B

## Q6(pdf Q#141)
한 회사가 전 세계 속보, 지역 알림, 날씨 정보를 제공하는 웹 기반 포털을 운영하고 있습니다. 이 포털은 정적 콘텐츠와 동적 콘텐츠를 혼합하여 각 사용자에게 맞춤형 보기를 제공합니다. 콘텐츠는 애플리케이션 로드 밸런서(ALB) 뒤에 있는 Amazon EC2 인스턴스에서 실행되는 API 서버를 통해 HTTPS로 제공됩니다.
이 회사는 전 세계 사용자에게 최대한 빠르게 콘텐츠를 제공하고자 합니다.
솔루션 아키텍트는 모든 사용자의 지연 시간을 최소화하기 위해 애플리케이션을 어떻게 설계해야 할까요?

A. 애플리케이션 스택을 단일 AWS 리전에 배포합니다. Amazon CloudFront를 사용하여 ALB를 오리진으로 지정하여 모든 정적 및 동적 콘텐츠를 제공합니다.
B. 애플리케이션 스택을 두 개의 AWS 리전에 배포합니다. Amazon Route 53 지연 시간 라우팅 정책을 사용하여 가장 가까운 리전의 ALB에서 모든 콘텐츠를 제공합니다.
C. 애플리케이션 스택을 단일 AWS 리전에 배포합니다. Amazon CloudFront를 사용하여 정적 콘텐츠를 제공합니다. 동적 콘텐츠는 ALB에서 직접 제공합니다.
D. 애플리케이션 스택을 두 개의 AWS 리전에 배포합니다. Amazon Route 53 지리적 위치 라우팅 정책을 사용하여 가장 가까운 리전의 ALB에서 모든 콘텐츠를 제공합니다.

기능	                 설명
Edge location	        전세계 수백개
dynamic content 가속	 가능
HTTPS 지원	             기본
ALB origin 가능	         가능
TCP 최적화	             있음

CloudFront 동작

사용자 → 가까운 Edge → AWS backbone → ALB

인터넷 전체 경로보다
AWS 내부망이 훨씬 빠르다.

정답 : A

## Q7(pdf Q#217)
한 회사가 애플리케이션 로드 밸런서 뒤의 Amazon EC2 인스턴스에서 글로벌 웹 애플리케이션을 운영하고 있습니다. 이 애플리케이션은 Amazon Aurora에 데이터를 저장합니다.
이 회사는 재해 복구 솔루션을 구축해야 하며 최대 30분의 다운타임과 잠재적인 데이터 손실을 허용할 수 있습니다.
또한, 기본 인프라가 정상 작동 중일 때는 솔루션이 부하를 처리할 필요가 없습니다.
이러한 요구 사항을 충족하기 위해 솔루션 아키텍트는 무엇을 해야 할까요?

A. 필요한 인프라 요소를 갖춘 상태로 애플리케이션을 배포합니다. Amazon Route 53을 사용하여 액티브-패시브 페일오버를 구성합니다.
두 번째 AWS 리전에 Aurora 복제본을 생성합니다.
B. 두 번째 AWS 리전에 애플리케이션의 축소 배포를 호스팅합니다. Amazon Route 53을 사용하여 액티브-액티브 페일오버를 구성합니다.
두 번째 리전에 Aurora 복제본을 생성합니다.
C. 두 번째 AWS 리전에 기본 인프라를 복제합니다. Amazon Route 53을 사용하여 액티브-액티브 페일오버를 구성합니다. 최신 스냅샷에서 복원되는 Aurora 데이터베이스를 생성합니다.
D. AWS Backup을 사용하여 데이터를 백업합니다. 백업을 사용하여 두 번째 AWS 리전에 필요한 인프라를 생성합니다. Amazon Route 53을 사용하여
액티브-패시브 페일오버를 구성합니다. 두 번째 리전에 Aurora 두 번째 기본 인스턴스를 생성합니다.

Active-passive + Aurora cross-region replica

두번째 리전 DR 준비
Route53 failover routing
Aurora replica 생성
장애 시 failover

정답 : A
## Q8(pdf Q#224)
최근 한 회사가 웹 애플리케이션을 AWS로 마이그레이션하여 단일 AWS 리전의 Amazon EC2 인스턴스에 애플리케이션을 재호스팅했습니다.
이 회사는 애플리케이션 아키텍처를 고가용성 및 내결함성을 갖도록 재설계하고자 합니다. 트래픽은 실행 중인 모든 EC2 인스턴스에 무작위로 접근해야 합니다.
이러한 요구 사항을 충족하기 위해 회사가 취해야 할 조치는 무엇입니까? (두 가지를 선택하십시오.)

A. Amazon Route 53 페일오버 라우팅 정책을 생성합니다.
B. Amazon Route 53 가중치 라우팅 정책을 생성합니다.
C. Amazon Route 53 다중값 응답 라우팅 정책을 생성합니다.
D. EC2 인스턴스 세 개를 시작합니다. 하나는 한 가용 영역에, 하나는 다른 가용 영역에 배치합니다.
E. EC2 인스턴스 네 개를 시작합니다. 하나는 한 가용 영역에, 나머지 두 개는 다른 가용 영역에 배치합니다.

정책	     특징
Failover	장애 시 전환만
Weighted	비율 분배
Latency	    지연 기반
Geo	        위치 기반
Multivalue	여러 healthy IP 랜덤 반환

모든 인스턴스에 랜덤으로 트래픽
→ Multivalue answer routing

2 AZ 각각 2개
균형 구조

AZ 하나 죽어도:
2개 남음
서비스 유지

정답 : C ,E

## Q9(pdf Q#264)
한 회사가 Amazon Route 53을 통해 트래픽이 관리되는 10개의 Amazon EC2 인스턴스에 웹 애플리케이션을 호스팅하고 있습니다. 이 회사는 애플리케이션에 접속하려고 할 때 가끔 타임아웃 오류가 발생합니다.
네트워킹 팀은 일부 DNS 쿼리가 비정상적인 인스턴스의 IP 주소를 반환하여 타임아웃 오류가 발생하는 것을 발견했습니다.
솔루션 아키텍트는 이러한 타임아웃 오류를 해결하기 위해 무엇을 구현해야 할까요?

A. 각 EC2 인스턴스에 대해 Route 53 단순 라우팅 정책 레코드를 생성하고 각 레코드에 상태 확인을 연결합니다.
B. 각 EC2 인스턴스에 대해 Route 53 장애 조치 라우팅 정책 레코드를 생성하고 각 레코드에 상태 확인을 연결합니다.
C. EC2 인스턴스를 원본으로 하는 Amazon CloudFront 배포를 생성하고 EC2 인스턴스에 상태 확인을 연결합니다.
D. EC2 인스턴스 앞에 상태 확인이 있는 애플리케이션 로드 밸런서(ALB)를 생성하고 Route 53에서 ALB로 라우팅합니다.

Route53
  ↓
ALB
  ↓
EC2 10대

health check 자동

ALB가:
unhealthy EC2 자동 제외
healthy로만 트래픽
→ timeout 제거

DNS 캐시 문제 없음
사용자는:
ALB DNS만 접근

ALB가 내부에서:
healthy EC2 선택

정답 : D

## Q10(pdf Q#265)
솔루션 아키텍트는 웹, 애플리케이션 및 데이터베이스 계층으로 구성된 고가용성 애플리케이션을 설계해야 합니다. HTTPS 콘텐츠 전송은
최소한의 전송 시간으로 가능한 한 에지(Edge)에 가깝게 이루어져야 합니다.
다음 중 이러한 요구 사항을 충족하고 가장 안전한 솔루션은 무엇입니까?

A. 퍼블릭 서브넷에 여러 개의 중복 Amazon EC2 인스턴스를 사용하여 퍼블릭 애플리케이션 로드 밸런서(ALB)를 구성합니다.
Amazon
CloudFront를 구성하여 퍼블릭 ALB를 오리진(Origin)으로 사용하여 HTTPS 콘텐츠를 전송합니다.
B. 프라이빗 서브넷에 여러 개의 중복 Amazon EC2 인스턴스를 사용하여 퍼블릭 애플리케이션 로드 밸런서(ALB)를 구성합니다.
Amazon
CloudFront를 구성하여 EC2 인스턴스를 오리진으로 사용하여 HTTPS 콘텐츠를 전송합니다.
C. 프라이빗 서브넷에 여러 개의 중복 Amazon EC2 인스턴스를 사용하여 퍼블릭 애플리케이션 로드 밸런서(ALB)를 구성합니다.
Amazon
CloudFront를 구성하여 퍼블릭 ALB를 오리진으로 사용하여 HTTPS 콘텐츠를 전송합니다.
D. 퍼블릭 서브넷에 여러 개의 중복 Amazon EC2 인스턴스를 사용하여 퍼블릭 애플리케이션 로드 밸런서를 구성합니다. Amazon CloudFront를 구성하여 EC2 인스턴스를 오리진으로 사용하여 HTTPS 콘텐츠를 제공합니다.

사용자
 ↓
CloudFront (엣지)
 ↓
ALB (public)
 ↓
EC2 (private subnet)
 ↓
DB (private)

CloudFront:
전세계 edge location
HTTPS termination
가장 빠른 전달

정답 : C

## Q11(pdf Q#302)
한 회사가 사용자가 모바일 기기에서 슬로우 모션 비디오 클립을 스트리밍할 수 있는 모바일 앱을 개발하려고 합니다. 현재 이 앱은 비디오 클립을 캡처하여 원본 파일 형식으로 Amazon S3 버킷에 업로드합니다. 앱은 S3 버킷에서 이러한 비디오 클립을 직접 가져옵니다.
하지만 원본 형식의 비디오 파일 크기가 매우 큽니다.
이로 인해 사용자는 모바일 기기에서 버퍼링 및 재생 문제를 겪고 있습니다. 회사는 운영 오버헤드를 최소화하면서 앱의 성능과 확장성을 극대화하는 솔루션을 구현하고자 합니다.
다음과 같은 솔루션 조합 중 어떤 것이 이러한 요구 사항을 충족할까요? (두 가지를 선택하세요.)

A. 콘텐츠 전송 및 캐싱을 위해 Amazon CloudFront를 배포합니다.
B. AWS DataSync를 사용하여 비디오 파일을 AWS 리전의 다른 S3 버킷에 복제합니다.
C. Amazon Elastic Transcoder를 사용하여 비디오 파일을 더 적절한 형식으로 변환합니다.
D. 콘텐츠 전송 및 캐싱을 위해 로컬 영역에 Amazon EC2 인스턴스의 자동 확장 그룹을 배포합니다.
E. 비디오 파일을 더 적절한 형식으로 변환하기 위해 Amazon EC2 인스턴스의 자동 확장 그룹을 배포합니다.

CloudFront = CDN
콘텐츠 전송 최적화

기능:
전세계 Edge 캐싱
모바일 가까운 위치에서 전송
버퍼링 감소
대역폭 최적화

모바일 스트리밍 → CloudFront 거의 필수

정답 : A, C
## Q12(pdf Q#367)
한 회사가 Amazon Route 53의 지연 시간 기반 라우팅을 사용하여 전 세계 사용자를 위한 UDP 기반 애플리케이션 요청을 라우팅하고 있습니다.
이 애플리케이션은 미국, 아시아, 유럽에 있는 회사 온프레미스 데이터 센터의 이중화 서버에 호스팅됩니다. 회사의
규정 준수 요건에 따라 애플리케이션은 온프레미스에 호스팅되어야 합니다. 회사는 애플리케이션의 성능과 가용성을 향상시키고자 합니다.
솔루션 아키텍트는 이러한 요건을 충족하기 위해 무엇을 해야 할까요?

A. 온프레미스 엔드포인트를 처리하기 위해 세 개의 AWS 리전에 세 개의 네트워크 로드 밸런서(NLB)를 구성합니다. AWS Global Accelerator를 사용하여 가속기를 생성하고,
이 NLB들을 해당 가속기의 엔드포인트로 등록합니다. 가속기 DNS를 가리키는 CNAME 레코드를 사용하여 애플리케이션에 대한 액세스를 제공합니다.
B. 온프레미스 엔드포인트를 처리하기 위해 세 개의 AWS 리전에 세 개의 애플리케이션 로드 밸런서(ALB)를 구성합니다. AWS Global Accelerator를 사용하여 가속기를 생성하고,
이 ALB들을 해당 가속기의 엔드포인트로 등록합니다. 가속기 DNS를 가리키는 CNAME 레코드를 사용하여 애플리케이션에 대한 액세스를 제공합니다.
C. 온프레미스 엔드포인트를 처리하기 위해 세 개의 AWS 리전에 세 개의 네트워크 로드 밸런서(NLB)를 구성합니다. Route 53에서 세 개의 NLB를 가리키는 지연 시간 기반 레코드를 생성하고, 이를 Amazon CloudFront 배포의 오리진으로 사용합니다. CloudFront DNS를 가리키는 CNAME 레코드를 사용하여 애플리케이션에 대한 액세스를 제공합니다.
D. 온프레미스 엔드포인트를 처리하기 위해 세 개의 AWS 리전에 세 개의 애플리케이션 로드 밸런서(ALB)를 구성합니다. Route 53에서 세 개의 ALB를 가리키는 지연 시간 기반 레코드를 생성하고, 이를 Amazon CloudFront 배포의 오리진으로 사용합니다. CloudFront DNS를 가리키는 CNAME 레코드를 사용하여 애플리케이션에 대한 액세스를 제공합니다.

사용자
 ↓
Global Accelerator (anycast IP)
 ↓
각 Region NLB
 ↓
온프레 서버

UDP 지원

NLB → UDP 가능
Global Accelerator → UDP 가능

정답 : A

## Q13(pdf Q#408)
한 회사가 UDP를 사용하는 지리적으로 분산된 수천 개의 원격 장치에서 데이터를 수신하는 애플리케이션을 운영하고 있습니다. 이 애플리케이션은
데이터를 즉시 처리하고 필요한 경우 장치로 메시지를 다시 보냅니다. 데이터는 저장되지 않습니다.
이 회사는 장치에서 장치로의 데이터 전송 지연 시간을 최소화하는 솔루션이 필요합니다. 또한 이 솔루션은 다른 AWS 리전으로의 빠른 장애 조치를 제공해야 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

A. Amazon Route 53 장애 조치 라우팅 정책을 구성합니다. 두 리전 각각에 네트워크 로드 밸런서(NLB)를 생성합니다. NLB가
데이터를 처리하기 위해 AWS Lambda 함수를 호출하도록 구성합니다.
B. AWS Global Accelerator를 사용합니다. 두 리전 각각에 엔드포인트로 네트워크 로드 밸런서(NLB)를 생성합니다. Fargate 시작 유형을 사용하는 Amazon Elastic
Container Service(Amazon ECS) 클러스터를 생성합니다. 클러스터에 ECS 서비스를 생성합니다. ECS 서비스를 NLB의 대상으로 설정합니다.
Amazon ECS에서 데이터를 처리합니다.
C. AWS Global Accelerator를 사용합니다. 두 리전 각각에 엔드포인트로 애플리케이션 로드 밸런서(ALB)를 생성합니다. Fargate 시작 유형을 사용하는 Amazon
Elastic Container Service(Amazon ECS) 클러스터를 생성합니다. 클러스터에 ECS 서비스를 생성합니다. ECS 서비스를 ALB의 대상으로 설정합니다.
Amazon ECS에서 데이터를 처리합니다.
D. Amazon Route 53 장애 조치 라우팅 정책을 구성합니다. 두 리전 각각에 애플리케이션 로드 밸런서(ALB)를 생성합니다.
Fargate 시작 유형을 사용하는 Amazon Elastic Container Service(Amazon ECS) 클러스터를 생성합니다. 클러스터에 ECS 서비스를 생성합니다. ECS 서비스를 ALB의 대상으로 설정합니다.
Amazon ECS에서 데이터를 처리합니다.

UDP 지원

NLB → UDP 지원
Global Accelerator → UDP 지원

Global Accelerator:
AWS backbone network 사용
nearest edge 접속
인터넷 경로보다 빠름

ECS Fargate:
서버 관리 없음
auto scaling
운영 최소

정답 : B

## Q14(pdf Q#461)
한 회사가 단일 AWS 리전에서 모바일 게임 앱을 개발하고 있습니다. 이 앱은 Auto Scaling 그룹의 여러 Amazon EC2 인스턴스에서 실행됩니다.
회사는 앱 데이터를 Amazon DynamoDB에 저장합니다. 앱은 사용자와 서버 간에 TCP 트래픽과 UDP 트래픽을 사용하여 통신합니다.
이 애플리케이션은 전 세계적으로 사용될 예정입니다. 회사는 모든 사용자에게 가능한 한 낮은 지연 시간을 보장하고자 합니다.
이러한 요구 사항을 충족하는 솔루션은 무엇일까요?

A. AWS Global Accelerator를 사용하여 액셀러레이터를 생성합니다. Global Accelerator 통합을 사용하고 TCP 및 UDP 포트에서 수신 대기하는 액셀러레이터 엔드포인트 뒤에 Application Load Balancer(ALB)를 생성합니다.
Auto Scaling 그룹을 업데이트하여 인스턴스를 ALB에 등록합니다.
B. AWS Global Accelerator를 사용하여 액셀러레이터를 생성합니다. Global Accelerator 통합을 사용하고 TCP 및 UDP 포트에서 수신 대기하는 액셀러레이터 엔드포인트 뒤에 Network Load Balancer(NLB)를 생성합니다.
Auto Scaling 그룹을 업데이트하여 인스턴스를 NLB에 등록합니다.
C. Amazon CloudFront 콘텐츠 전송 네트워크(CDN) 엔드포인트를 생성합니다. 엔드포인트 뒤에 Network Load Balancer(NLB)를 생성하고
TCP 및 UDP 포트에서 수신 대기합니다. Auto Scaling 그룹을 업데이트하여 인스턴스를 NLB에 등록합니다. CloudFront가 NLB를
오리진으로 사용하도록 업데이트합니다.
D. Amazon CloudFront 콘텐츠 전송 네트워크(CDN) 엔드포인트를 생성합니다. 엔드포인트 뒤에 애플리케이션 로드 밸런서(ALB)를 생성하고 TCP 및 UDP 포트에서 수신 대기합니다. Auto Scaling 그룹을 업데이트하여 인스턴스를 ALB에 등록합니다. CloudFront를 업데이트하여 ALB를 오리진으로 사용합니다.

게임 앱 = GA 대표 사례
gaming
real-time
UDP
-> GA

정답 : B

## Q15(pdf Q#464)
한 회사가 온라인 쇼핑 애플리케이션을 운영하고 있으며, 모든 주문 정보는 Amazon RDS for PostgreSQL 단일 가용 영역(Single-AZ) DB 인스턴스에 저장됩니다. 경영진은
단일 장애 지점을 제거하고자 하며, 애플리케이션 코드 변경 없이 데이터베이스 다운타임을 최소화할 수 있는 방안을 솔루션 아키텍트에게 요청했습니다.
다음 중 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

A. 기존 데이터베이스 인스턴스를 수정하고 다중 가용 영역(Multi-AZ) 옵션을 지정하여 다중 가용 영역 배포로 변환합니다.
B. 새로운 RDS 다중 가용 영역 배포를 생성합니다. 현재 RDS 인스턴스의 스냅샷을 생성하고, 해당 스냅샷을 사용하여 새로운 다중 가용 영역 배포를 복원합니다.
C. 다른 가용 영역에 PostgreSQL 데이터베이스의 읽기 전용 복제본을 생성합니다. Amazon Route 53 가중 레코드 세트를 사용하여 요청을 데이터베이스 전체에 분산합니다.
D. RDS for PostgreSQL 데이터베이스를 최소 그룹 크기가 2인 Amazon EC2 Auto Scaling 그룹에 배치합니다. Amazon Route 53 가중 레코드 세트를 사용하여 요청을 인스턴스 전체에 분산합니다.

modify DB → enable Multi-AZ

장점:
기존 endpoint 유지
코드 변경 없음
다운타임 최소
자동 failover
SPOF 제거

## Q16(pdf Q#527)
한 회사가 단일 AWS 리전에서 운영되는 지역 구독 기반 스트리밍 서비스를 보유하고 있습니다. 아키텍처는 Amazon EC2 인스턴스의 웹 서버와 애플리케이션 서버로 구성됩니다.
EC2 인스턴스는 Elastic Load Balancer 뒤의 Auto Scaling 그룹에 속해 있습니다. 이 아키텍처에는
여러 가용 영역에 걸쳐 확장된 Amazon Aurora 글로벌 데이터베이스 클러스터가 포함됩니다.
이 회사는 글로벌 확장을 계획하고 있으며, 애플리케이션의 다운타임을 최소화하고자 합니다.
다음 중 어떤 솔루션이 가장 높은 내결함성을 제공할까요?

A. 웹 계층과 애플리케이션 계층의 Auto Scaling 그룹을 확장하여 두 번째 리전의 가용 영역에 인스턴스를 배포합니다.
Aurora 글로벌 데이터베이스를 사용하여 기본 리전과 두 번째 리전에 데이터베이스를 배포합니다. Amazon Route 53 상태 확인을 사용하고
두 번째 리전으로의 장애 조치 라우팅 정책을 설정합니다.
B. 웹 계층과 애플리케이션 계층을 두 번째 리전에 배포합니다. 두 번째 리전에 Aurora PostgreSQL 교차 리전 Aurora 복제본을 추가합니다.
Amazon Route 53 상태 확인을 사용하고 두 번째 리전으로의 장애 조치 라우팅 정책을 설정합니다. 필요에 따라 보조 인스턴스를 기본 인스턴스로 승격합니다.
C. 웹 계층과 애플리케이션 계층을 두 번째 리전에 배포합니다. 두 번째 리전에 Aurora PostgreSQL 데이터베이스를 생성합니다. AWS
Database Migration Service(AWS DMS)를 사용하여 기본 데이터베이스를 두 번째 리전으로 복제합니다. Amazon Route 53 상태 확인을 사용하고
두 번째 리전으로의 장애 조치 라우팅 정책을 설정합니다.
D. 웹 계층과 애플리케이션 계층을 두 번째 리전에 배포합니다. Amazon Aurora 글로벌 데이터베이스를 사용하여 기본 리전과 보조 리전에 데이터베이스를 배포합니다. 장애 조치 라우팅 정책을 사용하여 보조 리전으로 Amazon Route 53 상태 확인을 수행합니다. 필요에 따라 보조 리전을 기본 리전으로 승격합니다.

구성:

1️. 웹/app → 두 Region 배포
2️. Aurora global DB → primary + secondary
3️. Route53 health check
4️. 장애 시 secondary promote

Aurora Global DB DR
특징:
replication < 1초
빠른 promote
최소 데이터 손실
최소 downtime

정답 : D

## Q17(pdf Q#538)
글로벌 비디오 스트리밍 회사가 Amazon CloudFront를 콘텐츠 전송 네트워크(CDN)로 사용하고 있습니다. 이 회사는 여러 국가에 걸쳐 콘텐츠를 단계적으로 배포하려고 합니다.
콘텐츠가 배포되는 국가 외부에 있는 시청자는 해당 콘텐츠를 시청할 수 없도록 해야 합니다.
다음과 같은 솔루션이 이러한 요구 사항을 충족할까요?

A. 허용 목록을 사용하여 CloudFront의 콘텐츠에 지역 제한을 추가합니다. 사용자 지정 오류 메시지를 설정합니다.
B. 제한된 콘텐츠에 대한 새 URL을 설정합니다. 서명된 URL과 쿠키를 사용하여 액세스를 승인합니다. 사용자 지정 오류 메시지를 설정합니다.
C. 회사가 배포하는 콘텐츠의 데이터를 암호화합니다. 사용자 지정 오류 메시지를 설정합니다.
D. 제한된 콘텐츠에 대한 새 URL을 생성합니다. 서명된 URL에 대한 시간 제한 액세스 정책을 설정합니다.

Geo restriction (국가 제한)

두 가지 방식:
allow list → 특정 국가만 허용
block list → 특정 국가 차단

문제 요구:
특정 국가만 먼저 rollout
→ allow list

허용 국가: 시청 가능
그 외 국가: 자동 차단

custom error message 설정 가능
운영 간단
CloudFront native 기능

정답 : A