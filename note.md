# Basic
## Region : 지역
AWS의 모든 서비스가 위치하는 물리적인 장소

## AZ(Avalability Zone) : 가용 역역
Region내에 위치한 데이터 센터(Information Data Center: IDC) 
AZ 하나가 down 되더라도 서비스 가능(무중단 서비스 제공)  

## IOPS(Input/Output Operations Per Second)
HDD, SDD 등 저장장치의 속도를 나타내는데 사용되는 측정 단위로 초당 처리되는 I/O 개수

---

# RDS(Relational Database Service)
AWS Cloud에서 DBMS를 쉽게 설정(set up), 운영(operate), 확장(scale)할 수 있는 웹 서비스

!RDS 개념도!

## 특징
- You can use the database products you are already familiar with: MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL Server.
- Amazon RDS manages backups, software patching, automatic failure detection, and recovery.
- You can turn on automated backups, or manually create your own backup snapshots.  
  You can use these backups to restore a database.  
  The Amazon RDS restore process works reliably and efficiently.
- You can get high availability with a primary instance and a synchronous secondary instance that you can fail over to when problems occur.  
  You can also use read replicas to increase read scaling.
- In addition to the security in your database package, you can help control who can access your RDS databases by using AWS Identity and Access Management (IAM) to define users and permissions. 
  You can also help protect your databases by putting them in a virtual private cloud (VPC).

## DB Instances
 AWS Cloud에서 독립적인 database 환경이며 RDS에서의 기본 단위
 
### Engines
- MySQL
- MariaDB
- PostgreSQL
- Oracle
- Microsoft SQL Server

### Storage
MySQL, MariaDB, Oracle, PostgreSQL은 64TiB 까지, SQL Server는 16TiB 까지 용량 생성 가능
#### Type
- SSD(Grneral Purpose : gp2) 
  - DBMS 워크로드에 비용적으로 효율적으로 사용하기 위한 Storage
  - I/O 성능 : 1GiB 당 3IOPS이며 최소 100IOPS, 1TiB는 3000IOPS
- PIOPS(Provisioned IOPS : io1)
  - 빠르고 일관된 I/O 성능이 필요한 경우 사용
- Magnetic(standard)  
  - 이전 버전과 호환하기 위한 Storage

### Replication
원본 DB Instance에서 읽기 전용 복제본의 replication 생성

</br>

# EC2(Clastic Compute Cloud)
가상 서버를 제공하는 서비스
- Instance : 가상 컴퓨팅 환경

## 기본 개념
- Start : OS가 부팅되고 사용할 수 있는 상태, 1시간 단위로 사용 요금 과금
- Stop : OS가 종료되어 Instance가 종료된 상태, 미과금
- Terminate : Instance가 삭제된 상태
- Reboot : OS가 종료 후 다시 시작하는 상태
- Root Device : OS가 설치되는 스토리지, EBS와 Instance Storage 를 사용할 수 있음
- Kernel ID : Instance가 이용하는 Linux Kernel
  - Linux Kernel : OS Kernel 수정 가능, 반가상화(Paravirtualization)
  - Windows Kernel : OS Kernel 수정 불가, 하드웨어가상화(HVM), 전가상화(Full Virtualization)

</br>

# EBS(Elastic Block Storage)
EC2 Instance에서 사용하는 block 수준의 가상 저장 장치  
빠르게 접근하고 장기적인 지속성이 필요한 데이터의 경우 사용

## 특징
- 암호화된 Volume 생성 가능
- snapshot 생성 가능
- snapshot을 생성후 Region 어느 곳에서나 새 볼륨으로 복원 가능 > 지리적 확장, IDC 마이그레이션, 재해복구

## 종류
- Grneral Purpose SSD Volume(gp2/gp3) 
  - 비용 차원에서 효율적으로 사용 시 적합
- Provisioned IOPS SSD Volume(io1/io2)
  - 일관성 있는 I/O 집약적 workload 사용 시 적합
  - 일관된 IOPS 제공
- Throughput Optimized HDD Volume(st1)
  - 저비용 Magnetic Storage
  - 대용량 순처 workload에 적합
- Cold HDD Volume(sc1)
  - 저비용 Magnetic Storage
  - 데이터에 자주 접근하지 않고 비용을 절약해야하는 경우 사용


## 기본 개념
- Volume : EBS의 가장 기본으로 OS에서 사용 가능한 형태
- AMI(Amazon Machine Image: Image) : OS가 설치된 상태, Instance 생성 시 사용
- Snapshot : EBS Volume을 특정 시점 복사한 파일, EBS Volume과 AMI 생성 가능
- Block : Unix/Linux에서 저장 장치로부터 읽고 쓰는 기본 단위

</br>

# S3(Simple Storage Service)
확장성, 데이터 가용성, 보안 및 성능을 제공하는 객체 스토리지 서비스
파일을 저장하여 HTTP 프로토콜로 접근 가능

## 특징
- 저장 용량이 무한으로 용량 추가하지 않아도 됨
- 파일 저장에 최적화가 되어있어 성능을 높이는 작업 필요없음
- EC2와 EBS로 구축하는 것보다 저렴
- 정적 웹사이트 구축에 용이
- 자동확장(Auto Scaling)rhk qngkrotjs(Load Balancing) 지원

## 기본 개념
- Bucket :  S3에서의 Object를 저장 공간으로 최상위 폴더
  - 최대 100개 생성 가능
  - 생성 후 이름 또는 Region 변경 불가
  - Naming Rules
    - 길이 : 3 ~ 63자
    - 소문자와 숫자, .(dots), -(hyphens)만 가능
    - 첫 자와 끝자는 소문자 또는 숫자로 구성
    - IP format 불가
    - xn--로 시작(nx--xxxx) 불가
    - -s3alias로 마감(xxxx-s3alias) 불가
    - Region에서 유일
    - S3 Transfer Acceleration을 사용하는 Bucket은 이름에 .(dots) 사용 불가
- Object : Bucket에 저장되는 기본 Entity
  - Object data와 Metadata로 구성
  - 1 object 당 최대 5TB까지 사용 가능
  - 기본 개념
    - Key : 사용자가 명명한 object의 이름
    - Value : object의 내용(데이터)
    - Version ID : Object 추가 시 S3에서 생상하는 string
    - Metadata : Object를 설명하는 key-value의 집합
      - 마지막 수정 날짜와 같은 기본 metadata와 Content-Type 형식의 Standard HTTP metadata를 포함
      - 확장자에 따라 자동 설정
      - Key-Value 형태
      - S3 전용 Metadata 및 사용자 정의 Metadata로 저장

</br>

# DynamoDB
NoSQL 데이터 베이스 서비스

## 특징
- Region 별로 생성
- 높은 내구성 : 여러 AZ에 자동 복제
- 높은 가용성 : 자동 분산 처리하며 일관되고 빠른 성능 유지
- 용량 제한 없음

# IAM(Identity & Access Management : 식별 및 접근 관리)
AWS Resource에 대한 접근을 제어할 수 있는 서비스
Resource를 사용할 수 있도록 인증, 권한 부여된 대상 제어

root 사용자 : AWS를 처음 생성할때 생기는 모든 AWS Service, Resource에 완전한 접근 권한이 있는 SSO(Single Sign-In) ID

## 특징
- 모든 Region에 동일하게 사용
- 부서별로 AWS 계정 분리 가능
- Role : 특정 Resource에 대한 권한

# ELB(Elastic Load Balancing)
둘 이상의 AZ에서 EC2 Instance, Containor, IP 주소 등 여러 대상에 걸쳐 수신되는 트래픽을 분산해주는 서비스
등록된 대상의 상태를 모니터링하여 양호한 상태의 대상으로만 트래픽 라우팅 수행

## 기본 개념
- L4(OSI Layer 4) : 전송 계층으로 TCP, UDP가 대표적이며 IP:port로 트래픽 분배
- L7(OSI Layer 7) : 애플리케이션 계층으로 HTTP Header 기준으로 트래픽 분배
- Load Balancing Algorithm : 트래픽을 EC2로 분배 시 사용하는 Algorithm, Round-Robin 사용
  - Round-Robin : 우선순위 없이 순서대로 분배
- Heath Check : 정상 가동 확인하는 기능, 비정상 시 트래픽 분배 대상에서 제외
- Connection Draining : Auto Scaling이 사용자의 요청을 처리중인 EC2 Instance를 삭제하지 못하도록 방지
- Sticky Session : 사용자의 Session을 확인하여 EC2 Instance로 트래픽을 분재, HTTP Coockie 사용
- Latency : ELB - EC2 Instance간의 지연 시간
- Surge Queue Length : ELB에서 EC2 Instance로 분배되지 못하고 Qeueu에 대기중인 Request 수
- Spillover Count : Surge Queue Full로 ELB가 거부한 Request 수
- Pre-warning : 트래픽 증가를 예상하여 미리 처리량 증가 요청 
