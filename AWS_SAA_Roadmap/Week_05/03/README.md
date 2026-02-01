# Placeholder
Q138.

정답: A

Q178.

정답: D

Q182.

정답: B

Q187.

정답: B,E

Q193.

정답: B

Q241.

정답: B

Q268.

정답: A

Q273.

정답: A

Q276.

정답: A,D

Q458.

정답: B,C

Q537.

정답: A

오답!!

Q138: B

Amazon MQ + Amazon RDS

Queue: RabbitMQ를 EC2에 직접 설치해서 운영하는 것보다 Amazon MQ를 쓰는 것이 훨씬 편하다

Database: Amazon RDS는 “Multi-AZ” 옵션만 켜면 AWS가 알아서 이중화를 해주므로 운영 부담이 줄어든다

Q178: A

AWS Backup을 사용해서 통합관리, 크로스 리전 복사, 가장 적은 노력의 조건을 만족한다

Q187: A, D

데이터베이스: Amazon RDS Multi-AZ → 고 가용성을 위한 기능

컨테이너: ECS with Fargate Launch type → serverless 컨테이너 서비스

Q241: C

Multi-AZ는 단일 리전 안에서 복제하는 기술

Q273: B

pilot light → DB만 켜두고 EC2는 꺼져있는 상태

warm stanby → 애플리케이션 서버도 최소한의 규모로 실행되고 있는 상태