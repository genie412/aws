# Basic
## Region : 지역
AWS의 모든 서비스가 위치하는 물리적인 장소

## AZ(Avalability Zone) : 가용 역역
Region내에 위치한 데이터 센터(Information Data Center: IDC) 
AZ 하나가 down 되더라도 서비스 가능(무중단 서비스 제공)  

## IOPS(Input/Output Operations Per Second)
HDD, SDD 등 저장장치의 속도를 나타내는데 사용되는 측정 단위로 초당 처리되는 I/O 개수이다.

</br>

---

</br>

# RDS(Relational Database Service)
AWS Cloud에서 DBMS를 쉽게 설정(set up), 운영(operate), 확장(scale)할 수 있는 웹 서비스이다.  

## Advantages
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
 AWS Cloud에서 독립적인 database 환경이며 RDS에서의 기본 단위이다.
 
### Engines
- MySQL
- MariaDB
- PostgreSQL
- Oracle
- Microsoft SQL Server

### Storage
MySQL, MariaDB, Oracle, PostgreSQL은 64TiB 까지, SQL Server는 16TiB 까지 용량 생성 가능하다.
#### Type
- SSD(Grneral Purpose : gp2)  
  최대 3000 IOPS 가능하다.  
- PIOPS(Provisioned IOPS : io1)
- Magnetic(standard)