# MySQL

## 공부자료
[x] [생활코딩-DB1](https://opentutorials.org/course/3162)

[x] [생활코딩-DB2](https://opentutorials.org/course/3161)

[x] [생활코딩-SQL Join](https://opentutorials.org/course/3884)

[x] [프로그래머스-MySQL](https://programmers.co.kr/learn/challenges)

[x]  [생활코딩-Relational data modeling](https://www.youtube.com/playlist?list=PLuHgQVnccGMDF6rHsY9qMuJMd295Yk4sa)
## 데이터베이스의 목적
관계형 데이터베이스 -> 표의 형태로 표현
- spreadsheet랑 비슷함.

## 설치 및 작동
mysql community edition download>MySQL Community Server>DMG archive
cd /usr/local/mysql/bin
./mysql -uroot -p 

## MySQL의 구조
표(table)
database - 표들을 grouping (schema)
- 연관된 데이터를 grouping
데이터베이스 서버에 저장

database server > database, schema, > table

## 서버 접속
./mysql u___ 
- u___ 사용자
- uroot 관리자

## 스키마의 사용
schema(database) 만들기
- CREATE DATABASE opentutorials;

delete database
- DROP DATEBASE opentutorials;

- SHOW DATABASES;

USE opentutorials;
- mysql은 지금부터 opentutorials에있는 schema를 표를 대상으로 명령을 실행

## SQL과 테이블의 구조
SQL - Structured Query Language
row,record - data 자체
column - data의 타입

## 테이블의 생성
create table in mysql cheat sheet
type을 지정할 때 최대값에 가까운것을 선택

- CREATE TABLE topic(
    id INT(11) NOT NULL AUTO_INCREMENT,
    title VARCHAR(100) NOT NULL,
    description TEXT NULL,
    created DATETIME NOT NULL,
    author VARCHAR(30) NULL,
    profile VARCHAR(100) NULL,
    PRIMARY KEY(id)
);

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
모든 정보
- SELECT * FROM topic;

*mysql SELECT syntax*

SELECT id,title,created,author FROM topic;

SELECT id,title,created,author FROM topic WHERE author='jihoon';


SELECT id,title,created,author FROM topic WHERE author='jihoon' ORDER BY id DESC;

SELECT id,title,created,author FROM topic WHERE author='jihoon' ORDER BY id DESC LIMIT 2;


## UPDATE
UPDATE topic SET description='Oracle is ...', title='Oracle' WHERE id=2;

## DELETE
DELETE FROM topic WHERE id = 5;

## 관계형데이터베이스의 필요성
- 중복 데이터의 관리.
- 그리고 그 각각의 데이터들의 용량이 크다면..
- 유지보수가 용이

테이블의 분리 tradeoff
- 해당 행의 표를 비교하면서 봐야함.

꿈 
- 중복을 발생하지 않으면서 하나의 표로 합쳐진 데이터를 보는 것
데이터를 분산시키지만,합쳐서 보여준다



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
 
INSERT INTO `author` VALUES (1,'egoing','developer');
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
테이블을 읽을 때 하나의 테이블로 저장되어진 것처럼 보이게 만들 수 있다

SELECT * FROM topic LEFT JOIN author ON topic.author_id = author.id;

SELECT topic.id, title, description, created,name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;

SELECT topic.id AS topic_id, title, description, created,name, profile FROM topic LEFT JOIN author ON topic.author_id = author.id;

중복을 제거하는 것.

SELECT * FROM comment LEFT JOIN author ON comment.author_id = author.id;
SELECT comment.id, description, name, profile FROM comment LEFT JOIN author ON comment.author_id = author.id;

## 인터넷과 데이터베이스
database client를 통해 database server에 접속
- 기존 강의에서는 mysql monitor
- MySQL workbench (GUI)

## MySQL Workbench
./mysql -uroot -p -h127.0.0.1

-h
-> facebook.com, google.com...


## further study
SQL, Index, modeling, backup, cloud

backup
- mysqldmup, binary log


# JOIN - part 2
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
- 왼쪽에 있는 것과 오른쪽에 같이 있는 것 나오고, 그 다음에 각자 있는 것 조인

EXCLUSIVE JOIN
- A에만 존재하는 것을 찾아내는 것

주의점: JOIN에서 병목현상이 일어날 수 있다.


# Relational data modeling

## Intro
Model - 어떤 목적을 가지고 진짜를 모방하는 것 (좋은 모델 = 목적에 부합하는 모방)
목적 - 표에 정보를 닮는 것, but data가 너무 많음.
data modeling <- 누구든 데이터를 닮을 수 있는 방법을 모안
- 복잡한 현실을 컴퓨터로 이사 시키는 것

## 전체 흐름
업무파악 -> 개념적 데이터 모델링(ER digram) -> 논리적 데이터 모델링 (표로 전환) -> 물리적 데이터 모델링 (실제 SQL)

업무파악
- 하려는 일을 파악 

개념적 모델링
- 하고자하는 일에 대한 개념과 그 관의 상호작용 (ER diagram)

논리적 데이터 모델링
- 관계형 데이터 베이스 표로 전환

물리적 데이터 모델링
- 어떤 데이터베이스 제품을 선택하고, 그 데이터베이스에 최적화된 코드를 작성해서 표를 만드는 것.

## 업무파악
컴퓨터 자체의 문제 - 데이터베이스를 만든다
현실의 문제 - 데이터베이스를 통해 현실의 문제를 해결, 아이디어를 구현


## 기획
와이어프레임 툴로 시각화.

## 개념적 데이터 모델링
파악한 업무에서 개념을 뽑아 내는 것.
( 논리적 데이터 모델링, 물리적 데이터 모델링을 하고 다시 돌아오면 쉽게 이해될 것 )

Entity Relationship Diagram
- 정보
- 그룹 (연관된 정보의 그룹핑)
- 관계 (정보 그룹 사이의 관계) 
-> 쉽게 표로 전환 할 수 있음

## 관계형 데이터베이스 다운 개념의 구조 
RDB에서는 표안의표 즉 내포관계를 허용하지 않는다, 
거대 단일 테이블로 표현을 하면 중복이 발생한다,
-> 주제에 따라 테이블을 나눈다, 그리고 query문을 통해 원하는 데이터를 얻는다.

## ERD의 구성요소
Entity는 네모, 속성은 원

Entity (개념적 모델) -> 후에 Table로 전환
- 글이라는 entity -> 그 안의 정보 (제목,본문,생성일)
구체적인 데이터 -> Attribute or 속성
-> 후에 column이 된다.

 -> - - -  쓰다 - - - <- 
저자 -쓰다 - 글 - 소속 - 댓글
- Relation(PK, FK, JOIN)
- Entity 관의 연관성을 표현 해준 것 -> Relation

Entity -> Table
Attribute -> Column
Relation -> PK, FK
Tuple -> Row (그리고 행 )

## Entity 정의
기획서에서 Entity를 찾아내야함. (읽기 화면보다는, 쓰기 화면에서 찾기가 쉬움)

Entity 추출!
저자, 글, 댓글


## 속성 정의

제목, 작성일, 본문 (글)

이름, 자기소개, 가입일 (저자)

본문, 작성일 (댓글)

## Idetifier(식별자) 지정
ex) 자동차번호, 도메인, 주빈등록번호 
-> 원하는 대상을 정확히 타겟팅, 다른 데이터와 겹치면 안된다.

candidate key -> 식별자가 될 수 있는 키들
- 중복값을 지니지 않은 것.

primary key -> candidate keys중 선택되어진 키.
- 나머지는 alternate key(대체 키)가 됨. -> 추후에 성능 향상을 위해 index?로 사용 가능한듯?

composite key (중복키)
- 두 가지 데이터를 함께 사용해야 식별할 수 있는 것.

ER diagram에 밑줄 = primary key

(저자 아이디, 글아이디, 댓글아이디) 추가 -> 각 entity가 자신의 식별자를 확인할 수 있는 식별자를 생성.

## Relationship (Entity간의 연갈)
foreign key
- 외래에 있는 테이블과 연괄할 떄 쓰는 열쇠 외래키
relationship이란 
- primary key와 foregin key가 연결되는 것을 통해 구현된다.

relationship은 마름모 꼴

저자 - 작성 - 글 // 저자 - 작성 - 댓글 // 글 - 소속 - 댓글

## Cardinality
1 - 1
담임 - 반 (각 선생님은 한 반만 담임한다)
반 - 담인 (각 반의 담인은 한명이다)     검은네모 - 검은네모


1 - N
저자 - 댓글 (각 저자는 여러 글을 작성한다)
댓글 - 저자 (각 댓글은 하나의 저자만 존재한다) 검은네모 -<(삼발이) 검은네모

N - M
저자 - 글 (각 저자는 여러 글을 작성한다)    검은네모 >-< 검은네모
글 - 저자 (각 글은 여러 저자가 존재한다)
- 이 경우 연결 테이블을 사용하여, 1 - N 관계로 converting 하여 구현

## Optionality
저자에게 댓글은 option이다.

저자 - 댓글 (저자는 댓글을 작성하지 않을수도 있다)  검은네모 -o 검은네모
댓글 - 저자 (각 댓글은 반드시 저자가 있다)        검은네모 |-o 검은네모 (| mandatory)


## 논리적 데이터 모델링
개념적 모델링 - 개념을 뽑아내는일
논리적 데이터 모델링 - 뽑아낸 개념을 관계형 데이터베이스 패러다임에 어울리게 데이터 형식을 정리정돈

Mapping Rule - ER Digram을 통해서 표현한 내용을 관계형 데이터베이스로 전환할 때 쓰는 방법론
네모 - Entity -> Table
동그라미 - Attribute -> Column
마름모 - Relation -> PK, FK

## 테이블과 컬럼
1. Entity를 Table로
- Foregin key가 없는 테이블 먼저하면 좋은듯?

-저자-
- id(pk), name, profile, created, 
- int   ,VarChar,VarChar,datetime
- NN,    NN       NN      NN 
-글-

-댓글-


## 1:1 관계의 처리
부모 (저자 - 휴먼저자) 자식 휴먼저자는 저자에게 의존 
저자 Primarty, 휴먼저자 Foreign key 

## 1:N 관계의 처리

## N:M 관계의 처리
어느 쪽이든 column을 추가하기가 어려움

mapping table을 만듦
-write-
author_id, topic_id, created


## 정규화 (Normalization)
정제되지 않은 데이터를 관계형 데이터베이스에 어울리는 표로 만드는 레시피.

UNF - unnomalizedform
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
-> 중복키가 없어야 한다.

## Third Normal Form
- No transitive dependencies
- foregin key는 중복이라고 치지 않는다

## 물리적 데이터 모델링
이상적인 표를 구체적인 제품에 맞는 현실적인 표로 만드는 것(성능)
"find slow query"

normalized된 form을 성능을 위해 denormalization
- 그 전에 고려해봐야함. 
- Index -> 행에 대한 읽기 성능을 향상시키고 쓰기 성능을 하향시킴 + 저장 공간이 더 많이 듦 but 빠름
- application 영역에서 cache 사용
- 그래도 안되면 denormalization

## denormalization
정규화를 통해서 만든 표를 성능이나 개발의 필요성에 의해 조작하는 것
- 정규화 -> 대체로 쓰기의 편리함을 위해 읽기를 희생하는 것 (표를 쪼개고 후에 Join을 사용해야 하기 때문)
- 하지만, 꼭 정규화를 하고 역정규화를 해야하는 것

http://bit.ly/2WLMCko

## 역정규화 : 컬럼을 조작해서 join을 줄이기
- join을 안해도 되서 더 빠름
- 대신 normalization 하기 전의 문제가 다시 생김(중복)
- 시스템의 복잡도가 높아짐(성능을 위해..?)

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

