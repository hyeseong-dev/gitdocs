# ERROR

6월 5일 

서버 오류  


Server info

```text
인스턴스 ID
i-0f1e7a300af6c163d
퍼블릭 DNS(IPv4)
ec2-3-22-225-2.us-east-2.compute.amazonaws.com
인스턴스 상태
running
IPv4 퍼블릭 IP
3.22.225.2
인스턴스 유형
t2.micro
IPv6 IP
-
결과
권장 사항을 위해 AWS Compute Optimizer에 옵트인합니다. 자세히 알아보기
탄력적 IP
프라이빗 DNS
ip-172-31-35-20.us-east-2.compute.internal
가용 영역
us-east-2c
프라이빗 IP
172.31.35.20
보안 그룹
launch-wizard-2. 인바운드 규칙 보기. 아웃바운드 규칙 보기
보조 프라이빗 IP
예약된 이벤트
예약된 이벤트 없음
VPC ID
vpc-76bf631d
AMI ID
ubuntu/images/hvm-ssd/ubuntu-bionic-18.04-amd64-server-20200408 (ami-07c1207a9d40bc3bd)
서브넷 ID
subnet-ba0298f6
Platform details
Linux/UNIX
네트워크 인터페이스
eth0
Usage operation
RunInstances
IAM 역할
-
소스/대상 확인
예
키 페어 이름
Docker_Tutorial
T2/T3 무제한
비활성
소유자
697245288584
EBS 최적
아니요
시작 시간
2020년 5월 27일 오후 4시 8분 12초 UTC+9(241시간)
루트 디바이스 유형
ebs
종료 방지
아니요
루트 디바이스
/dev/sda1
수명 주기
normal
블록 디바이스
/dev/sda1
모니터링
기본
Elastic Graphics ID
-
경보 상태
없음
Elastic Inference 액셀러레이터 ID
-
커널 ID
-
용량 예약
-
RAM 디스크 ID
-
용량 예약 설정
열기
Outpost ARN
-
배치 그룹
-
파티션 번호
-
가상화
hvm
예약
r-0bb9f2b8a7fa31180
AMI 시작 인덱스
0
테넌시
default
호스트 ID
-
호스트 리소스 그룹 이름
-
선호도
-
상태 전환 이유
-
상태 전환 이유 메시지
-
최대 절전 중지 동작
비활성
vCPU 수
로드 중...
```

### 현상 1 

ssh 접속 불가 

![](../../.gitbook/assets/image%20%28228%29.png)

현상2 

[http://aws.hkit.xyz ](http://aws.hkit.xyz%20) 개설된 도메인 접속 불가   
  
방법 : 

1\) 원인 파악 후 에러 사항 해결   
장점 : 추후 동일 문제를 동일 패턴으로 빠르게 해결 가능   
단점 : 문제 원인 파악과 해결책을 찾는것에 상당한 시간이 소요될 것으로 파악함. 

2\) 기존 EC2 인스턴스 삭제후 새인스턴스 생성  
장점: 바로 해결 가능한 장점   
단점: 소규모 프로젝트와 작은 서버에서만 가능하다는점. 더불어 추가 동일 문제 발생시 새로 인스턴스를 생성해야한다는 점  


#### 해결 방법 

 - 기존 EC2 서버인스턴스 삭제후 새 인스턴스 생성   








