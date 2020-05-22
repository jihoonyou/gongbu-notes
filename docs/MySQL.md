# MySQL

## 공부자료
[x] [생활코딩-DB1](https://opentutorials.org/course/3162)
[x] [생활코딩-DB2](https://www.opentutorials.org/module/4078)
[x] [생활코딩-SQL Join](https://opentutorials.org/course/3884)
[] [프로그래머스-MySQL](https://programmers.co.kr/learn/challenges)

[]  [생활코딩-Relational data modeling](https://www.youtube.com/playlist?list=PLuHgQVnccGMDF6rHsY9qMuJMd295Yk4sa)
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