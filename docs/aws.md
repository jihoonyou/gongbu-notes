# Amazon Web Services

## 공부자료
[] [생활코딩](https://opentutorials.org/course/2717)


## 아마존 서비스와 클라우드
일반 - 컴퓨터에 프로그램을 설치하여 작업 처리
클라우드 컴퓨팅 - 구름위에 있는 컴퓨터를 이용하여 작업 처리 (구름:인터넷의비유)
- 인터넷에 연결되어있는 거대한 컴퓨터를 연결하여 사용한다

Amazon Web Service안의 상품 하나하나가, 거대한 컴퓨터

1년간 프리티어 무료 (하지만, 일정 제한이 있음)
기업, 개발자, 무료.. 등급으로 

새로 사용자를 만들어서 안전하게 사용권장

## 보안설정
IAM - Identity and Access Management에서 보안 설정

Activate MFA on your root account
- otp 앱으로 사용하는 거 추천. (스마트폰)
 - 스마트폰 잃어버렸을 경우.. 인증부분에서 고객 서비스팀에 문의

## 지역과 가용구역
지역(Region) - AWS의 컴퓨터의 위치
- 소비자와 지역의 위치를 고려해야함
- 거리가 멀수록 경유지를 통해 가는 중 병목현상이 발생할 수 있음 => 느려짐
- 한국에서 개발을 하지만, 고객들은 남미쪽이라면.. 인프라를 도쿄가 아닌 상 파울로쪽으로 해야함.
- 각 지역마다 같은 상품을 쓰더라도 가격이 다를 수 있음 (환율 등 여러가지 요건)
- [속도측정](http://www.cloudping.info) latency(지연시간 측정)
 -  현재 위치의 측정이지 제 3의 지역에 측정은 아님

가용구역(Availablity zone)
하나의 region에 여러개의 건물이 있음
- 여러개의 건물이 떨어져 있는 이유 -> 비상시 백업, 안정장치
- 지역하나에 여러개의 가용구역, 각각의 건물들이 있음 -> 인터넷보다 빠른 전용선으로 연결되어 있음.

지역-지역은 직접적 연결 - X
같은 지역안에 가용구역끼리 빠르게 데이터 주고받기 가능 
- 서로 다른 지역도 가능하지만 같은 az처럼 빠르진 않음
   region                region
(az-전용선-az)---인터넷---(az-전용선-az)

## EC2 소개
지역 설정
독립된 컴퓨터 한 대를 통채로 빌려주는 것
instance - 컴퓨터 한대 
컴퓨터 생성!

## EC2 인스턴스 타입
instances - launch instance
- Choose AMI
 - 임대할 컴퓨터의 운영체제를 설치하는 것
   - UNIX를 뿌리로하는 LINUX or SUSE Linux, Ubuntu, Windows Server 2012
   - Windows 중 SQL server가 설치되어 있는 것은 무료가 아님
- Choose an Instance Type
 - 임대할 컴퓨터의 사양을 선택
 - Type => 컴퓨터의 성능을 나타냄
 - vCPUs => virtual CPU
 - cpu에 우위가 있는 것이 앞에 c가 붙고, memroy가 우위에 있는 것이 m이 붙어 있음

## EC2 가격정책
EC2 instance 요금에서 가격정책 확인

on demand instance
- 필요할 때 키고 필요할 때 끄는 것

예약 instance
- 할인권 느낌?
- 서버의 경우, 1년내내 끌 필요없다 => 최대 75%할인

스팟 인스턴스
- 노는 컴퓨터가 많을 때, 가격이 저렴. 노는 컴퓨터가 없으면 일반 인스턴스보다 가격이 높아질 수 있음

## EC2 인스턴스 장치 설정
Configure Instance
- number of instances => 몇개의 인스턴스를 만들까
- request Spot instances를 체크해서 스팟 인스턴스 설정 (가변적인 요금)
- 그 밑에 네트워크 관련 설정을 할 수 있음
- shutdown behavior => 운영체제에서 컴퓨터를 종료했을 때, stop or terminate
- termination protection => 실수로 인스턴스를 삭제하는 것을 방지
- monitoring => CPO의 monitoring을 디테일하게 저장하여 확인가능
 - (Adiitiuonal charges apply - 체크하면 돈이 들어간다)

Add Storage
- 컴퓨터의 저장장치를 장착하는 것
- elastic block store
- size 30GB까지 무료. 
- Volume type => 해당 저장장치가 어떤 타입인가. 
 - Provisioned IOPS로 직접적으로 속도 설정가능 
 - General Purpose, Magnetic
- Delte on Termination 
 - 이 저장장치는 인스턴스와 분리되어있는 저장장치. instance가 삭제되면, 저장장치를 폐기 같이 되게 안되게 설정가능 (외장하드, 내장하드 느낌?)

## EC2 태그와 보안그룹
Tag Instance
- 인스턴스를 만들면 그 인스턴스가 어떤역할인지, 누가 관리한지 메모 

Configure Security Group
- 보안관련 방화벽
- 해당 인스턴스의 접속을 허용하고 막는 것
- 제한된 방법들만 네트워크를 통해 인스턴스를 제어하게 가능
- Type 
 - SSH => 만드는 네트워크가 리눅스 계열에 허용 (리눅스의 원격제어 설정!)
 - source => SSH를 통해서 인스턴스의 접속을 허용하는데
  - Anywhere 모든거를 허용
  - My IP - 해당 사무실에서만 또는 집에서만 허용하는 것 (해당 IP만 허용)
 - 웹 서버로는 HTTP로 설정
  - HTTP에 My IP로 설정하면, 집이나 오피스에서만 오피스를 접속하게만 허용하는 것 하지만 웹 서비스는 WWW의 전 세계 사람들이 접속하게 하는 것이기 때문에, 개인접속만 하면 이상 so choose anywhere
   - 다른 특정 IP의 접속을 허용해주고 싶으면, Custom IP로 지정해주면 됨
 - windows의 원격제어의 경우는, RDP로 설정

## EC2 인스턴스 비밀번호 생성
인스턴스에 네트워크를 통해서 접속할 때, 사용할 비밀번호 지정하는 화면.
- 복잡함 비밀번호라서 (머리로 기억 못할) 파일로 저장됨
- 비밀번호의 이름을 저장
 - Download Key Pair하면 AWS에서 랜덤하게 생성
 - 이 파일을 잘 저장해야함, 잃어버리면 절대 AWS에서 돌려주지 않음
 
## EC2 리눅스 인스턴스 접속
오른쪽 클릭 conenct
- Open an SSH client
 - Mac OS => terminal 
- chmod 400 aws_password.pem
 - 404 - 이 파일의 소유자만 읽을 수 있고, 소유자가 아니면 존재 자체도 알 수 없음
 - 오른쪽 클릭하여 '정보가져오기'에서 직접 바꿀 수 있음
- ssh -i "aws_password.pem" ubuntu@ec2-54-180-115-193.ap-northeast-2.compute.amazonaws.com
 - ssh => 접속할 때 사용하는 프로그램
 - -i "aws_password.pem"=> 로그인 파일을 전송하여 제출하는 거
 - ubuntu@ec2-54-180-115-193.ap-northeast-2.compute.amazonaws.com => ubuntu가 아이디 // 인스턴스가 위치한 위치(ip)
 - EC2생성을 ubuntu로 안하였다면, ec2-user로 id를 바꿔야함
- exit으로 접속을 끔

리눅스에서
- sudo apt-get을 사용하여 프로그램을 쉽게 설치
- 해당 예제는 apache2 설정하여 서버사용
aws 보안설정
- 인스턴스-description-보안그룹-인바운드규칙보기
- 80이 전세계 사용자들 접속 허용

## EC2 윈도우 인스턴스 접속
RDP, HTTP

mirco remote Desktop를 앱스토어에서 다운
기존에 받은 비밀번호 파일로 로그인

## AWS를 제어하는 방법
Management Console (AWS)
- GUI 방식

CLI (Command Line Interface)
- aws ec2 describe-instances
 - aws중 ec2를 제어하겠다.
- 명령어를 통해 컴퓨터를 제어

SDK (Software Development Kit)
- 각각의 언어를 이용해서 aws의 각 인프라를 제어하는 것을 제공.
 - AWS를 프로그래밍적으로 제어하기 편리하도록 제공되는 라이브러리들을 의미합니다. 언어별로 다양한 라이브러리를 제공하고 있기 때문에 자신에게 맞는 라이브러리를 선택해서 사용하시면 됩니다. 

API (Application Programming Interface)
- 예시에서는 웹을 통한 Rest API를 사용


