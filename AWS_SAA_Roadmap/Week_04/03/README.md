# Placeholder
Q1.

정답: B

Q3.

정답: A

Q5.

정답: B

Q6.

정답: D

Q9.

정답: B

Q12.

정답: D

Q20.

정답: D

Q21.

정답: B

Q23.

정답: C

Q33.

정답: A

Q36.

정답: B

Q38.

정답: C

Q52.

정답: B

Q221.

정답: D

Q252.

정답: A

오답!!!

Q1: A

S3 Transfer Acceleration → 전 세계에 흩어진 edge location을 통해 aws 내부 네트워크로 빠르게전송한다 

Q5: C

EBS는 단일 인스턴스만 적용이된다. 이 경우 EFS를 사용해야한다. 

Q6: B

Snowball Edge → 인터넷을 전혀 사용하지 않음

Q12: A

CloudFront에 S3와 ALB를 모두 오리진으로 등록한다

- S3는 정적데이터를 저장하여 데이터를 caching함
- ALB는 동적데이터를 저장하여 AWS 글로벌 백본 네트워크를 타고 오리진까지 최단 경로를 연결한다

Q21: D

EC2+ALB+RDS = 3-tier architecture이지만, ec2는 overhead가 큼

D는 serverless architecture를 사용함

Q23: B

S3 Glacier Deep Archive는 스토리지 클래스 중 가장 저렴하다

Q33: C

DynamoDB는 민감정보를 삭제해주는 rule이 없다

KDS를 통해 트랜잭션을 실시간으로 수집하고, AWS Lambda 민감 정보를 삭제한 뒤, db에 넣는 로직을 수행

Q52. C

Amazon EFS: NFS를 제공, 고가용성&확장성, Auto-scaling 지원