# MySQL

## 공부자료
[x] [생활코딩-DB1](https://opentutorials.org/course/3162)

[x] [생활코딩-DB2](https://opentutorials.org/course/3161)

[x] [생활코딩-SQL Join](https://opentutorials.org/course/3884)

[x] [프로그래머스-MySQL](https://programmers.co.kr/learn/challenges)

[x]  [생활코딩-Relational data modeling](https://opentutorials.org/course/3883)


## 데이터베이스의 목적
관계형 데이터베이스 -> 표의 형태로 표현
- spreadsheet랑 비슷함.

스프레드시트와 관계혀 데이터베이스의 차이점
- 클릭 vs 명령어


## 설치 및 작동
다운로드
- mysql community edition download>MySQL Community Server>DMG archive

터미널에서 사용시
- cd /usr/local/mysql/bin

mysql 서버 접속
- ./mysql -uroot -p 


## MySQL의 구조
표(table)
- 데이터를 기록하는 곳
- ex) 글을 저장하는 표, 댓글을 저장하는 표

database - 표들을 grouping (schema)
- 표가 많아진다면..
- 연관된 데이터를 grouping
- schema -> 표를 그룹힐할 때 사용하는 폴더
  - schema는 서로 연관된 데이터를 그룹핑 해준다.

데이터베이스 서버에 저장
- 스키마들을 저장
- mysql의 설치 -> 데이터베이스 서버라는 것을 설치 한 것
database server > database, schema, > table


## 서버 접속
권한등록가능
- 차등적으로 권한을 줄 수 있음
./mysql u___ -p
- u___ 사용자
  - ex) -ujihoon
- uroot 관리자


## 스키마의 사용
schema(database) 만들기
- CREATE DATABASE opentutorials;

delete database
- DROP DATABASE opentutorials;

- SHOW DATABASES;

USE opentutorials;
- mysql은 지금부터 opentutorials에있는 schema를 표를 대상으로 명령을 실행


## SQL과 테이블의 구조
SQL - Structured Query Language
- 언어
Query - 데이터베이스에게 질의
row, record, 행 - data 자체
column, 열 - data의 타입(구조)


## 테이블의 생성
create table in mysql cheat sheet -> 검색
[type을 지정할 때 최대값에 가까운것을 선택](https://www.techonthenet.com/mysql/datatypes.php)
- 항상 가장 큰 거를 사용하면 안됨 -> 저장 공간을 많이 차지하기 때문

- ``` CREATE TABLE topic(
    id INT(11) NOT NULL AUTO_INCREMENT,
    title VARCHAR(100) NOT NULL,
    description TEXT NULL,
    created DATETIME NOT NULL,
    author VARCHAR(30) NULL,
    profile VARCHAR(100) NULL,
    PRIMARY KEY(id)
);
    ```


(__)
- 보여지는 글자 수

NOT NULL
- 값이 없는 것을 허용하지 않는다.

NULL
- 값이 없는 것을 허용한다.

AUTO_INCREMENT
- 자동 증가

VARCHAR
- variable character

PRIMARY KEY
- 메인 키
- 중복방지, 성능

SHOW TABLES;

SET PASSWORD = PASSWORD('____');


## CRUD
Create
Read
Update
Delete


## INSERT
INSERT INTO tablename (v1,v2,v3,...)

DESC topic;
- 테이블 구조 확인

ex)
INSERT INTO topic (title,description,created, author, profile) VALUES('MySQL', 'MySQL is ...', NOW(),'Jihoon', 'developer');

ex)
SELECT * FROM topic;

## SELECT
모든 정보 출력
- SELECT * FROM topic;

[*mysql SELECT syntax*](https://dev.mysql.com/doc/refman/5.7/en/select.html)
- 대괄호 생략가능

SELECT id,title,created,author FROM topic;

SELECT id,title,created,author FROM topic WHERE author='jihoon';


SELECT id,title,created,author FROM topic WHERE author='jihoon' ORDER BY id DESC;

SELECT id,title,created,author FROM topic WHERE author='jihoon' ORDER BY id DESC LIMIT 2;


## UPDATE
UPDATE topic SET description='Oracle is ...', title='Oracle' WHERE id=2;


## DELETE
DELETE FROM topic WHERE id = 5;


## 관계형데이터베이스의 필요성
중복 데이터의 관리
- 개선이 필요하다
- 유지보수가 용이
- 각각의 데이터들의 용량이 크다면..
- 같은 이름, 같은 프로필이지만 id가 다르게 관리 가능

중복 데이터를 해결하는 방법
- 테이블의 분리
  -  단점(tradeoff) -> 해당 행의 표를 비교하면서 봐야함.

꿈 
- 데이터를 별도의 테이블로 보관하면서 중복을 발생시키지 않으면서 실제로 데이터를 볼 때,하나의 표로 합쳐진 데이터를 보는 것
- 데이터를 분산시키지만,합쳐서 보여준다 (저장은 분산, 데이터는 합쳐서) 


## 테이블 분리하기
RENAME TABLE topic TO topic_backup;


```
--
-- Table structure for table `author`
--


CREATE TABLE `author` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL,
  `profile` varchar(200) DEFAULT NULL,
  PRIMARY KEY (`id`)
);

--
-- Dumping data for table `author`
--

INSERT INTO `author` VALUES (1,'jihoon','developer');
INSERT INTO `author` VALUES (2,'duru','database administrator');
INSERT INTO `author` VALUES (3,'taeho','data scientist, developer');

--
-- Table structure for table `topic`
--

CREATE TABLE `topic` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `title` varchar(30) NOT NULL,
  `description` text,
  `created` datetime NOT NULL,
  `author_id` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
);

--
-- Dumping data for table `topic`
--

INSERT INTO `topic` VALUES (1,'MySQL','MySQL is...','2018-01-01 12:10:11',1);
INSERT INTO `topic` VALUES (2,'Oracle','Oracle is ...','2018-01-03 13:01:10',1);
INSERT INTO `topic` VALUES (3,'SQL Server','SQL Server is ...','2018-01-20 11:01:10',2);
INSERT INTO `topic` VALUES (4,'PostgreSQL','PostgreSQL is ...','2018-01-23 01:03:03',3);
INSERT INTO `topic` VALUES (5,'MongoDB','MongoDB is ...','2018-01-30 12:31:03',1);
```

## JOIN
분리된 테이블을 읽을 때 하나의 테이블로 저장되어진 것처럼 보이게 만들 수 있다

SELECT * FROM topic LEFT JOIN author ON topic.author_id = author.id;

SELECT topic.id, title, description, created,name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;

SELECT topic.id AS topic_id, title, description, created,name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;

SELECT * FROM comment LEFT JOIN author ON comment.author_id = author.id;
SELECT comment.id, description, name, profile FROM comment LEFT JOIN author ON comment.author_id = author.id;


## 인터넷과 데이터베이스
database client를 통해 database server에 접속

ndatabase client
- 기존 강의에서는 mysql monitor
- MySQL workbench (GUI)


## MySQL Workbench
./mysql -uroot -p -h127.0.0.1
- -hlocalhost -h127.0.0.1

-h
-> facebook.com, google.com...


## further study
SQL
- SELECT문에 대한 공부

Index
- 데이터가 엄청나게 많아질 때, 정리가 필요
- 사용자가 자주 쓰는 column에 색인을 건다
  - 빠르게 데이터를 처리할 수 있음 (성능상의 문제가 생길시 찾아볼 것)

modeling
- 데이터베이스의 설게

backup
- 데이터를 복제해서 보관(독립된 공간에 보관)
- 검색 키워드 mysqldmup, binary log

cloud
- 클라우드 컴퓨팅


# JOIN - part 2
여러개의 표로 분산된 정보를 결합하여 하나의 단일한 표로 만드는 것

[sql_join 연습장](http://bit.ly/join-exec)

https://sql-joins.leopard.in.ua/

https://docs.google.com/spreadsheets/d/1YN8mcTatO_X-azuSF5cjRUxfnyIcz-4q1IQVbn7I-k8/edit#gid=1849152573


LEFT OUTER JOIN
- A에만 있는정보 + B랑 겹치는거
- NULL 이 나온다는 것
  - 왼쪽에 있는 테이블에 값이 있는데 그 값에 해당하는 행이 오른쪽에는 없다.
RIGHT OUTER JOIN
- 동작 방법은 같지만 방향만 달라진 것.


INNER JOIN
- NULL 행이 존재하지 않음
- 일반적으로 성능이 더 좋음.
- 양쪽 모두에 있는 "행"


FULL OUTER JOIN
- 양 쪽에 있는 것 도 포함
- 합집합
- LEFT JOIN하고 RIGHT JOIN 그리고 중복 삭제
  - UNION에 중복을지우는 DISTINCT 키워드가 생략되어 있음
- 왼쪽에 있는 것과 오른쪽에 같이 있는 것 나오고, 그 다음에 각자 있는 것 조인
예시 
- SELECT * FROM topic FULL OUTER JOIN author ON topic.author_id = author.id
- outer join을 제공하지 않을 경우
  - (SELECT * FROM topic LEFT JOIN author ON topic.author_id = author.aid) UNION DISTINCT (SELECT * FROM topic RIGHT JOIN author ON topic.author_id = author.aid)


EXCLUSIVE JOIN
- A에만 존재하는 것을 찾아내는 것
예시
- SELECT * FROM topic LEFT JOIN author ON topic.author_id = author.aid WHERE author.aid is NULL;

주의점: JOIN에서 병목현상이 일어날 수 있다.
- explian 쿼리문 키워드를 앞에 붙여서 병목 지점을 찾아 볼 수 있음


# Relational data modeling

## Intro
Model - 어떤 목적을 가지고 진짜를 모방하는 것 (좋은 모델 = 목적에 부합하는 모방)
목적 - 표에 정보를 닮는 것, but data가 너무 많음.
data modeling <- 누구든 데이터를 닮을 수 있는 방법을 모안
- 복잡한 현실을 컴퓨터로 이사 시키는 것


## 전체 흐름
업무파악 -> 개념적 데이터 모델링(ER digram) -> 논리적 데이터 모델링 (표로 전환) -> 물리적 데이터 모델링 (실제 SQL)

업무파악
- 하려는 일을 파악 (의뢰한 사람과 알아내는 것. 의뢰한 사람이 무엇을 원하는지) 

개념적 모델링
- 하고자하는 일에 대한 개념과 그 개념안의 상호작용 (ER diagram)

논리적 데이터 모델링
- 관계형 데이터 베이스 표로 전환 (우리가 생각했던 개념을 표로 전환하는 것)

물리적 데이터 모델링
- 어떤 데이터베이스 제품을 선택하고, 그 데이터베이스에 최적화된 코드를 작성해서 표를 만드는 것. (코드로 실제표를 만드는 것 - SQL 코드)

데이터 모델링이란?
- 문제를 현실로부터 뜯어내서 고도의 추상화 과정을 거쳐서, 컴퓨터라는 새로운 현실로 옮겨 담는 작업


## 업무파악
컴퓨터 공학에서 해결하는 두 가지 문제
1. 컴퓨터 자체의 문제 - 데이터베이스를 만든다. (mysql, oracle을 만든다)
2. 현실의 문제 - 데이터베이스를 통해 현실의 문제를 해결, 아이디어를 구현 (ex. 데이터베이스를 통해서 인터넷 뱅킹 구현)


## 기획
와이어프레임 툴로 시각화.


## 개념적 데이터 모델링
파악한 업무에서 개념을 뽑아 내는 것.

Entity Relationship Diagram
- 정보(를 발견하고 표현할 수 있게 도와줌)
- 그룹 (서로 연관된 정보의 그룹핑하고 다른 사람에게 표현할 수 있게 해줌)
- 관계 (정보 그룹 사이의 관계를 인식하고 다른 사람에게 표현할 수 있게 해줌) 
- ERD를 쉽게 표로 전환 할 수 있음


## 관계형 데이터베이스 다운 개념의 구조 
RDB에서는 표안의 표, 즉 내포관계를 허용하지 않는다, 
거대 단일 테이블로 표현을 하면 중복이 발생한다,
- 해결방법: 주제에 따라 테이블을 나눈다, 그리고 query문을 통해 원하는 데이터를 얻는다.
- 장점: 주제에 따라 데이터를 그룹핑, 글에 대한 정보가 필요하다면 글에 대한 표만을 조회하여 자원을 아낄 수 있음, join을 통하여 합성하여 데이터를 가져올 수 있음.


## ERD의 구성요소
Entity (후에 Table로 전환)
- 글이라는 entity는 실제적인 데이터가 아니다
- 그 안의 정보 (제목,본문,생성일)가 구체적인 데이터 -> Attribute or 속성 (후에 표의 column이 된다)

entity들의 관계
 -> - - -  쓰다 - - - <- 
저자 - 쓰다 - 글 - 소속 - 댓글
- Relation(PK, FK, JOIN)
- Entity 관의 연관성을 표현 해준 것 -> Relation

□ Entity -> Table
○ Attribute -> Column
◇ Relation -> PK, FK
Tuple -> Row (그리고 행)


## Entity 정의
기획서에서 Entity를 찾아내야함. (읽기 화면보다는, 쓰기 화면에서 찾기가 쉬움)
Entity 추출!
- 저자, 글, 댓글


## 속성 정의
제목, 작성일, 본문 (글)
이름, 자기소개, 가입일 (저자)
본문, 작성일 (댓글)


## Idetifier(식별자) 지정
속성 중의 대표를 뽑는 것
ex) 자동차번호, 도메인, 주빈등록번호 
- 원하는 대상을 정확히 타겟팅
- 다른 데이터와 겹치면 안된다

candidate key(후보키) -> 식별자가 될 수 있는 키들
- 중복값을 지니지 않은 것.
- 기본키가 선택되면 나머지는 alternate key(대체키)
  - secondary index를 걸기 좋음

primary key(기본키) -> candidate keys중 선택되어진 키.
- 나머지는 alternate key(대체 키)가 됨. -> 추후에 성능 향상을 위해 index?로 사용 가능한듯?

composite key (중복키)
- 두 가지 데이터를 함께 사용해야 식별할 수 있는 것.

ER diagram에서의 밑줄 = primary key

(저자 아이디, 글아이디, 댓글아이디) 추가 -> 각 entity가 자신의 식별자를 확인할 수 있는 식별자를 생성.


## Relationship (Entity간의 연갈)
foreign key
- 외래에 있는 테이블과 연괄할 떄 쓰는 열쇠 외래키
relationship이란 
- primary key와 foregin key가 연결되는 것을 통해 구현된다.


□저자 - ◇작성 - □글 // □저자 - ◇작성 - □댓글 // □글 - ◇소속 - □댓글


## Cardinality
1 - 1
담임 - 반 (각 선생님은 한 반만 담임한다)
반 - 담인 (각 반의 담인은 한명이다)
■---■


1 - N
저자 - 댓글 (각 저자는 여러 글을 작성한다)
댓글 - 저자 (각 댓글은 하나의 저자만 존재한다)
■--<(삼발이)■


N - M
저자 - 글 (각 저자는 여러 글을 작성한다)    
글 - 저자 (각 글은 여러 저자가 존재한다)
■>-<■
- 실제로 DB table에서 표현할 수 없기 때문에, 이 경우 연결 테이블을 만들어서, 1 - N 관계로 converting 하여 구현


## Optionality
저자에게 댓글은 option이다.

저자 - 댓글 (저자는 댓글을 작성하지 않을수도 있다)  
■--o■

댓글 - 저자 (각 댓글은 반드시 저자가 있다)        
■-|-o■ (| mandatory)
■-|-o<■ (1 - N 이기 때문에)


## 논리적 데이터 모델링
개념적 모델링 - 개념을 뽑아내는 일
논리적 데이터 모델링 - 뽑아낸 개념을 관계형 데이터베이스 패러다임에 어울리게 데이터 형식을 정리정돈

Mapping Rule
- ER Digram을 통해서 표현한 내용을 관계형 데이터베이스로 전환할 때 쓰는 방법론
□ Entity -> Table
○ Attribute -> Column
◇ Relation -> PK, FK


## 테이블과 컬럼
ERD를 관계형 데이터 모델로 전환하는 작업을 진행
- ER Master사용해도 좋을듯

1. Entity를 Table로 변환
- Foregin key가 없는 테이블 먼저하면 좋은듯?

2. 속성을 만든다
-저자-
- id(pk), name, profile, created, 
- int   ,VarChar,VarChar,datetime
- NN,    NN       NN      NN 
-글-

-댓글-


## 1:1 관계의 처리
Relationship을 PK와 FK를 연결하는 것을 통해 관계형 데이터베이스 모델에 맞게 converting

저자 Primary key, 휴먼저자 Foreign key 
- 저자(부모테이블) - 휴먼저자 의존 없이 잘 지냄
- 휴먼저자(자식테이블) - 저자에게 의존


## 1:N 관계의 처리
저자와 댓글


## N:M 관계의 처리
저자와 글
- 어느 쪽이든 column을 추가하기가 어려움 (한 column에 여러개의 데이터가 들어가는 문제가 생겼기 때문에)

mapping table(중재자)을 만듦
- write 테이블을 생성
- [author_id, topic_id, created]


## 정규화 (Normalization)
정제되지 않은 데이터(표)를 관계형 데이터베이스에 어울리는 표로 만드는 레시피.

UNF - UnnomalizedForm
1NF - FirstNormalizedForm
...
6NF
- 주로 3NF까지 많이 사용
http://bit.ly/2wV2SFj


## First Normal Form
- Atomic columns
- 각 column의 값들이 하나하나가 atomic해야한다.
- 각각의 column이 값을 하나만 갖는다.


## Second Normal Form
- No partial dependencies
- 부분 종속성이 없어야한다
- 기본키 중에 중복키가 없어야 한다.


## Third Normal Form
- No transitive dependencies
- 이행적 종속성 없어야한다
- foregin key는 중복이라고 치지 않는다


## 물리적 데이터 모델링
이상적인 표를 구체적인 제품에 맞는 현실적인 표로 만드는 것(성능)
"find slow query"

normalized된 form을 성능을 위해 denormalization
- 그 전에 고려해봐야 될 것  
  - Index -> 행에 대한 읽기 성능을 향상시키고 쓰기 성능을 하향시킴 + 저장 공간이 더 많이 듦 but 빠름
  - application 영역에서 cache 사용
- 그래도 안되면 denormalization


## denormalization
정규화를 통해서 만든 이상적인 표를 성능이나 개발의 필요성에 의해 조작하는 것 (구조를 바꾸는 것)
- 정규화 -> 대체로 쓰기의 편리함을 위해 읽기를 희생하는 것 (표를 쪼개고 후에 Join을 사용해야 하기 때문)
  - join은 비싼 작업 
- 하지만, 꼭 정규화를 하고 역정규화를 해야하는 것

http://bit.ly/2WLMCko


## 역정규화 : 컬럼을 조작해서 join을 줄이기
- join을 안해도 되서 더 빠름
- 대신 normalization 하기 전의 문제가 다시 생김(중복)
- 시스템의 복잡도가 높아짐(성능을 위해..)


## 역정규화 : 컬럼을 조작해서 계산을 줄이기
계산값을 column에 추가 
ex) grouby count query를 매번 하지 않게


## 역정규화 : 표를 쪼개기
- 컬럼을 기준으로 표를 쪼개기
- topic // topic_description
- shadding(표 별로..? 컴퓨터를 나누어 각자 빠르게 처리하게)

- 행을 기준으로 표를 쪼개기
- topic_1000 // topic _2000


## 역정규화 : 관계의 역정규화
- Foreign key를 추가하여 join을 줄이는 것


```

```