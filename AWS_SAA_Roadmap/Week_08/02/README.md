# Week08 - KMS, WAF, Shield, Firewall Manager

## Q15

### 🧩 문제 요약

온프레미스에서 inspection 서버로 VPC 인바운드/아웃바운드 트래픽을 **검사(inspection)**하고 **필터링(filtering)**했다. AWS로 마이그레이션 후에도 동일한 기능을 VPC 경계에서 제공해야 한다.

### ✅ 정답

**C. Use AWS Network Firewall to create the required rules for traffic inspection and traffic filtering for the production VPC.**

### 🔍 정리

- 트래픽 검사/필터링은 AWS Network Firewall → VPC에 관리형 상태기반 방화벽을 배치해 L3–L7 규칙으로 인/아웃 트래픽 제어 가능

- 규칙 기반으로 inspection + filtering을 직접 구현 → 온프레미스 inspection 서버 역할을 가장 그대로 대체

## Q36

### 🧩 문제 요약

S3 버킷을 두 리전에 두고, 저장 데이터는 반드시 **KMS 고객 관리 키(CMK)**로 암호화해야 한다. 두 버킷의 데이터는 동일한 KMS 키로 암·복호화되어야 하며, 데이터와 키 모두 각 리전에 저장되어야 한다. 운영 오버헤드는 최소여야 한다.

### ✅ 정답

**B. Create a customer managed multi-Region KMS key. Create an S3 bucket in each Region. Configure replication between the S3 buckets. Configure the application to use the KMS key with client-side encryption.**

### 🔍 정리

- 키는 KMS Multi-Region customer managed key → “같은 키”를 두 리전에 동일한 키 ID/키 재질로 복제해 각 리전에 키가 존재하면서도 동일 키로 암·복호화 요구 충족

## Q80

### 🧩 문제 요약

EBS 기반 AMI가 KMS 고객 관리 키로 암호화된 스냅샷을 사용한다. 이 AMI를 MSP 파트너의 AWS 계정과 가장 안전하게 공유해야 한다.

### ✅ 정답

**B. Modify the launchPermission property of the AMI. Share the AMI with the MSP Partner's AWS account only. Modify the key policy to allow the MSP Partner's AWS account to use the key.**

### 🔍 정리

- AMI 공유는 launchPermission을 MSP 계정으로만 제한 공유 → 퍼블릭 공개 없이 최소 권한으로 배포

- 암호화 스냅샷은 원본 KMS CMK 권한이 있어야 사용 가능 → 키 정책에 MSP 계정 사용 권한 추가로 복호화/스냅샷 사용을 안전하게 허용

## Q100

### 🧩 문제 요약

EC2에서 컨테이너 앱이 다른 업무 앱과 통신하기 전에 보안 인증서(certs)를 다운로드해야 한다. 인증서는 근실시간으로 안전하게 암·복호화되어야 하고, 암호화 후 데이터는 고가용성 스토리지에 저장해야 한다. 운영 오버헤드는 최소여야 한다.

### ✅ 정답

**C. Create an AWS Key Management Service (AWS KMS) customer managed key. Allow the EC2 role to use the KMS key for encryption operations. Store the encrypted data on Amazon S3.**

### 🔍 정리

- 암·복호화는 AWS KMS CMK → 관리형 키로 근실시간 암호화/복호화 API 제공, 키 관리/보안 통제(권한·감사) 오버헤드 최소

## Q106

### 🧩 문제 요약

S3에 기밀 데이터를 저장한다. 요구사항은: 저장 시 암호화(Encryption at rest), 키 사용 로그 감사 가능, 키는 매년 회전, 운영 효율성 최대화

### ✅ 정답

**D. Server-side encryption with AWS KMS keys (SSE-KMS) with automatic rotation**

### 🔍 정리

- 암호화는 SSE-KMS → S3 저장 시 KMS 고객 관리 키로 암호화, 중앙 집중 키 관리 가능

- 감사 요구는 KMS + CloudTrail 통합 → 키 사용 내역(API 호출)이 로그로 기록되어 감사 요건 충족

- 키 회전은 KMS 자동 회전(annual automatic rotation) → 매년 자동으로 키 교체, 수동 운영 부담 최소

## Q119

### 🧩 문제 요약

API Gateway REST API가 us-east-1, ap-southeast-2 두 리전에 있고, **여러 계정(multi-account)**에 걸쳐 운영된다. SQLi/XSS로부터 보호해야 하며, 관리/운영 오버헤드는 최소여야 한다.

### ✅ 정답

**B. Set up AWS Firewall Manager in both Regions. Centrally configure AWS WAF rules.**

### 🔍 정리

- 공격 방어는 AWS WAF(SQLi/XSS 룰) → API Gateway Regional 엔드포인트에 Web ACL 연결로 보호 가능

## Q121

### 🧩 문제 요약

Multi-AZ로 운영 중인 암호화되지 않은 RDS가 있고, 매일 스냅샷을 찍고 있다. 앞으로는 DB와 스냅샷이 항상 암호화되도록 해야 한다.

### ✅ 정답

**A. Encrypt a copy of the latest DB snapshot. Replace existing DB instance by restoring the encrypted snapshot.**

### 🔍 정리

- 기존 비암호화 RDS는 “인플레이스 암호화 전환”이 불가 → 스냅샷을 암호화하여 복사한 뒤 그 암호화 스냅샷으로 복원해 새 암호화 DB로 교체해야 함

## Q165

### 🧩 문제 요약

CloudFront + S3 오리진으로 정적 웹사이트를 구성한다. 회사 정책상 모든 웹 트래픽은 반드시 AWS WAF를 거쳐 검사되어야 한다.

### ✅ 정답

**D. Configure Amazon CloudFront and Amazon S3 to use an origin access identity (OAI) to restrict access to the S3 bucket. Enable AWS WAF on the distribution.**

### 🔍 정리

- 트래픽 검사는 CloudFront에 AWS WAF 연결 → 모든 HTTP/HTTPS 요청이 엣지에서 WAF 규칙(SQLi/XSS 등) 검사 후 오리진 전달

## Q180

### 🧩 문제 요약

EC2 + NLB 뒤에서 동작하는 API 기반 플랫폼이 있고, 외부 접근은 API Gateway를 통해 제공된다.
요구사항: SQL Injection 등 웹 공격 방어, 대규모·정교한 DDoS 공격 탐지 및 완화

### ✅ 정답

**B. Use AWS Shield Advanced with the NLB.**
**C. Use AWS WAF to protect Amazon API Gateway.**

### 🔍 정리

- 웹 공격(SQLi, XSS 등) 방어는 AWS WAF를 API Gateway에 연결 → L7 레벨에서 요청 필터링, OWASP 룰 적용 가능

## Q189

### 🧩 문제 요약

계약서 문서를 5년 보관해야 하며, 그 기간 동안 삭제/덮어쓰기 불가(WORM) 여야 한다. 또한 저장 시 암호화, 암호화 키는 매년 자동 회전이 필요하고 운영 오버헤드 최소가 목표다. (2개 선택)

### ✅ 정답

**B. Store the documents in Amazon S3. Use S3 Object Lock in compliance mode.**
**D. Use server-side encryption with AWS Key Management Service (AWS KMS) customer managed keys. Configure key rotation.**

### 🔍 정리

- 변경 불가 보관은 S3 Object Lock (Compliance mode) → 보관 기간(5년) 동안 관리자라도 삭제/덮어쓰기 불가로 규정 준수형 WORM 충족

- 암호화/키 회전은 SSE-KMS + 고객 관리 키(CMK) 자동 회전 → 키 사용 감사(CloudTrail) + 연 1회 자동 회전으로 운영 부담 최소

## Q202

### 🧩 문제 요약

데이터를 S3로 이전한다. 저장 시 암호화가 필수이고, 암호화 키는 매년 자동 회전되어야 한다. 운영 오버헤드는 최소여야 한다.

### ✅ 정답

**B. Create an AWS Key Management Service (AWS KMS) customer managed key. Enable automatic key rotation. Set the S3 bucket’s default encryption behavior to use the customer managed KMS key. Move the data to the S3 bucket.**

### 🔍 정리

- 암호화는 **S3 기본 암호화(SSE-KMS)**로 강제 → 업로드되는 객체가 자동으로 KMS 키로 암호화
