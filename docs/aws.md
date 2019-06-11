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

##  EC2 AWS Marketplace
OS선택할 때, 실제로는 AMI로 아마존에서 만든 이미지.
- 다양한 이미지를 선택하여 해당 서비스를 pre-install된 환경에서 사용 가능

## EC2 Scalability - Scale Up
Scalability (변화하는 수요에 가용성을 변동시킴)
- 클라우드 컴퓨팅을 사용하여 사용자의 증가에 따라 빠르게 대응이 가능! (비용효율적)
- 하지만, 가상위에서 하는 거기때문에, 거기서 오는 기능저하 및 비용이 든다 
- 스타트업
 - 저렴한 컴퓨터사용 가능
 - nano로 수용가능
- 큰회사
 - 강력한 컴퓨터 사용
- 물리적인 컴퓨터가 해당 컴퓨터들을 생성해줌
- Scalabilty를 적용하는 두 가지 전략이 있음 Scale in, Scale up

Scale up
- 서버 그 자체를 증강하는 것에 의해서 처리 능력을 향상시키는 것
- 하나의 컴퓨터를 더 좋은 컴퓨터로 교체하는 것을 의미
- 수요에 따라 어떻게 탄력적으로 반응하는지
- top => CPU 점유율 확인

인스턴스 테스트 결과
- 동시접속자가 늘어나면, 개별처리속도가 느려짐
 - 즉 scale up이 필요한 상황이 생김

instance를 이미지화 시키고, 더 좋은 instance로 바꾸는 작업.
- stop을 시키고, instance를 다시 start하면 ip와 domain이 달라짐
- scale up을 하려면, 인스턴스의 상태를 freezing해서 image로 만들어야함
- Elastic ip - ip address를 아마존에서 받아서, 소유하는 것 (유료)
 - Release address로 삭제
 - Associate address로 ip를 부여할 인스턴스를 선택할 수 있음

인스턴스 교체
- create image
 - 해당 작업을 하면 인스턴스가 꺼짐. 그러므로 주의해야함.
 - AMI에 이미지가 만들어짐
  - 해당 이미지에 오른쪽 클릭 후, launch를 눌러서 인스턴스를 골라야 한다.
scale out은 scale up보다 좀 복잡해짐
- scale out은 적당한 규모가 되었을 때 고민 하는 것

## EC2 Scalability - Scale Out (ELB)
scale up - 수요에 따라서 더 좋은 컴퓨터로 업그레이드 하는 것.
- 단일 컴퓨터의 성능의 한계가 생길 수 있음.
scale out - 여러 컴퓨터를 연결하여 성능 향상.
- 복잡해짐.. 

Scale out의 흐름
- Web Server -> Middleware -> Database
- nginx,apache -> php,jsp,django-> mysql,nosql
- shadding등 데이터베이스, 미들웨어, 웹서버 등을 컴퓨터로 나눠서 여러 컴퓨터가 일처리를 하게 만듦
- 미들웨어 부분이 느려지면, 미들웨어 부분을 나눔.
- 웹서버의 과부화처리
 - DNS의 설정을 바꿔서, 서버를 나눠서 들어감.
 - load balancer를 써서, 웹 서버로 분산되게 함 => AWS에서는 ELB라고 불림

## ELB (Elastic Load Balancer)
Load Balancers 왼쪽 탭에서 Create Load Balancer
- ELB를 만들고, 기존의 인스턴스에 붙인다
앞단만 HTTPS/HTTP 설정하고 인스턴스는 그냥 HTTP로 통신해서 자원을 아낀다

Configure Health Check
- load balancer가 각각의 인스턴스에 사용자들의 요청을 분산해주는데, 특정 컴퓨터가 죽었는지 정기적으로 확인
- HTTP방식으로 80포트로 index.html로 접속했을 떄 해당 파일에 접속하지 못한다면, ELB는 해당 서버가 죽었구나 확인할 수 있음
- Advanced Details
 - response timeout 5 sec => 5초이상 걸리면 건강하지 않는다
 - Health Check Interval 30 sec => 30초마다 Health check를 하겠다
 - Unhealthy Threshold 2 => 위의 조건을 2번 충족못하면 죽었다고 생각하겠다
 - Healthy Threshold 10 => 죽어있는 상태에서 10번 시도해서 되면 살았다고 생각하겠다.
- Add EC2 Instances
 - 열어놓은 인스턴스를 선택

ELB적용
- Edit instance
인스턴스를 수동으로 늘렸다 줄이는 작업을 자동화하는 것이 auto-scaling
- ELB와 Auto-scaling을 같이하면 훨씬 강력해짐

ELB사용시 주의사항
- db가 다르면, 다른 화면이 보이게 되는 것을 주의
 - 그래서 DB를 분산하지 않는 예시를 보여줌 하지만 RDB 파트에서 DB 나누는 방법을 보여줄듯

## EC2 Scalability - Auto Scaling
필요에따라 자동으로 컴퓨터를 생성해서 컴퓨터를 시작했다가, 사용도가 떨어지면 자동으로 컴퓨터를 삭제하는 것

Launch Configurations
- 이미지를 인스턴스로 만드는 설정
 - my AMIS에서 생성한 이미지를 선택
 - 자동으로 인스턴스를 만들 때 어떤 이미지를 기반으로 만들지 정의
 
Auto Scaling Groups
- 언제 어떤 조건에서 만들것이냐
- Advanced Details
 - 자동으로 인스턴스에 자동으로 붙이는 방법
- Desired
 - 필요로 하는 인스턴스 숫자
- Instnaces
 - 현 인스턴스 숫자
- 어떤 인스턴스가 삭제될지 모름
  - 사용하고 버리는 느낌의 인스턴스 

Cloudwatch
- AWS에서 사용하고 있는 것을 확인할 수 있음.

SNS home
- Topics에서 삭제해야된다.
- Subscription부분도 삭제. 
ELB도 삭제

## nodejs를 위한 AWS SDK
aws sdk for javscript in node.js를 검색
- 개발자 안내
 - npm install aws-sdk --save
 - var AWS = require('aws-sdk');
- configuring the SDK in Node.js
 1. AWS.config
  - 모든 서비스에 적용되는 글로벌하게 configuration 적용
  - 
 2. passing extra configuration to s service object
  - 각각의 세부적인 설정
  - ex) S3는 서울 dynamo DB는 미국

Setting AWS Credentials
- 증명, 인증..
- 5가지의 증명 방법
 1. Loaded from IAM roles for Amazon EC2
  - NodeJS 애플리케이션이 EC2위에서 동작하는 상황이라면.. 가장 권장되는 방법? role을 설정 ID나 PW없이 crendential
 2. (~/./aws/credentials) 홈 디렉토리에 다음과 같이 정의하면, sdk동작할때 해당 파일이 있는지 확인하고 동작
 3. 환경변수 이용
 4. JSON파일을 따로 만들어서 이용
 5. 코드를 직접 하드코딩하는 방법

IAM => security&identity => users => 새로운 사용자 추가
- 새로운 id, key값 얻기
- 해당 id,key값을 잘 관리해야 한다.

common examples
- 여러 사례(예시)를 보고 실습.
api docs에서 어떻게 사용하는지 확인 (EC2사용법 등..)
에러를 console에 찍어서 확인.

user =>  permission  =>  attach policy
- AmazonEC2FullAccess 선택

## AWS S3
파일서버 서비스인 S3(Simple Storage Serivce)

S3 콘솔을 통한 기본 조작 방법
S3 -> Create Bucket
- 저장장치 생성
- 해당 버킷을 선택하여 어떤 파일이 있는지 확인 가능
- upload버튼으로 업로드 가능
 - 해당 파일을 클릭하면 보이는 링크를 통해 해당 파일에 접근가능
- 상대가 파일을 업로드하는 작업 등을 S3에 저장

Simple Storage Service
- 파일을 저장하는 서비스
- 객체 내구성(유실될 가능성)이 뛰어남 => 안전하다
