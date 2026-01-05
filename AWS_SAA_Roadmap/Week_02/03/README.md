# Placeholder
Virtual Private Cloud (VPC)

- AWS 클라우드 내에 논리적으로 격리된 사용자 전용 가상 네트워크 공간

CIDR: VPC의 IP 주소 범위를 지정한다

Subnet: VPC를더작은 단위로 쪼갠 것

- Public: 인터넷과 직접 통신 가능
- Private: 외부에서 직접 접근 불가, 내부 통신만 가능

Route table: 서브넷이 어떤 게이트웨이와 연결될지 결정한다

Gateway

- VPC는 기본적으로 외부와 차단되어 있는데, 외부와 통신하려면 적절한 게이트웨이를 연결해야함

A. Internet Gateway (IGW): VPC와 인터넷 간의 통신을 가능하게 하는 대문, VPC당 1개만 연결 가능하다

B. Network Adress Translation Gateway (NAT): Private Subnet에 있는 인스턴스가 인터넷으로 나갈 수 있게 해준다. 하지만 외부에서 들어오는 건 막는다, Public Subnet에 생성해야함

C. Egress-Only Internet Gateway: NAT Gateway와 같지만 IPv6 전용

D. Transit Gateway (TGW): 여러 개의 VPC와 온프레미스 네트워크를 연결하는 중앙 허브 역할을 한다

E. VPC Endpoint: 인터넷으로 타지 않고 AWS 내부 네트워크를 통해 S3과 DynamoDB에 접근하게 해준다

Q4.

정답: A

Q6.

정답: C

Q10.

정답: B

Q15.

정답: B

Q19.

정답: B

Q42.

정답: C
Q56.

정답: C
Q64.

정답: D

Q92.

정답: C, E

Q101.

정답: B

Q125.

정답: B, D

Q135.

정답: D

Q176.

정답: A

Q251.

정답: B

Q272.

정답: C

Q294.

정답: B

Q324.

정답: C

Q374.

정답: C

Q429.

정답: A

Q448.

정답: D

### 오답!

Q6.

C는 네트워크를 통해 전송하기 때문에 조건에 맞지 않음

B가 정답임 

Q92.

정답: A,C

EC2 인스턴스가인터넷을 거치지 않고S3에 가장 안전하게 접근하는 방법은 VPC Gateway endpoint를 사용하는 것

Q101.

정답: A

priavte subnet으로 두면 IGW 를 통해 밖으로 나갈 수 없어서 public을 사용해야함

Q125.

정답: A,E

EC2와 RDS를 private subnet에 배치하여 외부 노출을 막고, 가용성을 확보한다

ALB와 NAT Gateway는 무조건 public subnet에 두어야한다

Q272.

정답: B

API Gateway는 region 서비스 이기 때문에 글로벌과 맞지 않는다

반면에 Cloudfront는 전 세계에 퍼져있는 edge location을 통해 컨텐츠를 제공함

Q324.

Cached volume에 저장하면 cache에 없는 데이터는 S3에서 가져와야 하기 때문에 latency가 발생함

stored volume은 모든 데이터를 on-premise에 저장하기 때문에 latency가 발생하지 않고, 기존 iSCSI 방식을 그대로 사용해서 인프라 변경이 적음

Q374.

정답: D

3개의 connect를 생성하는 것은 비용이 많이 든다

TGW는 여러 VPC와 온프레미스 하나로 묶는 클라우드 라우터 역할을 한다

단일 direct connect를통해 TGW에 붙어 있는 모든 VPC가 온프레미스와 전용선으로 통신할 수 있다

 Q429.

allow 뒤의 문장은 적용되는 것이 아니라 모든 문장을 평가하여 결과를 낸다 (apply랑 deny를 헷갈림)

Q448.

정답: C

vpc peering은 고가용성이 보장되는 서비스로, 하나가 끊어진다고 통신이 두절되지는 않음

Management VPC에 대해 단일장비가 고장나면 SPoF이므로 두번째 gateway 장비를 추가하고 두 번째 VPN 세트를 연결하면 장비 이중화가 완성됨

 

### 필수 개념 정리!!

1. 네트워크 및 연결
    - S3/DynamoDB 사설 접근: Gateway VPC Endpoint
    - Saas 서비스 사설 연결: AWS Private Link (Interface VPC Endpoint)
    - Private Subnet의 인터넷 사용: NAT Gateway (Public subnet에 위치)
    - 다수 VPC + On-premise 연결: Transit Gateway
    - 글로벌 속도 개선: Amazon CloudFront
2. 스토리지 및 마이그레이션
    - 대용량데이터 오프라인 이동: AWS Snowball
    - Storage Gateway:
        - 모든 데이터: Stored Volume
        - 자주 쓰는 데이터: Cached Volume
3. 3Tier 아키텍쳐 정석 배치:
    - Public Subnet: ALB, NAT, Gateway
    - Private Subnet: EC2(App), RDS(DB)