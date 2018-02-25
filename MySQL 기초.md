# MySQL 기초

MySQL은 가장 널리 사용되고 있는 **관계형 데이터베이스 관리 시스템(RDBMS: Relational DBMS)**입니다. 

## Database

이 말을 이해하기 위해 먼저 데이터베이스, 관계형 데이터베이스가 무엇인지 이해해야 합니다. 데이터베이스란 한 마디로 구조화된 데이터의 집합입니다.  사용자는 데이터베이스를 통하여 효율적으로 데이터를 저장하고, 검색하고, 정렬하며, 탐색할 수 있게 됩니다. 우리가 흔히 쓰는 excel도 데이터베이스의 일종이라고 생각할 수 있습니다. 대부분의 회사나 기관에서는 데이터의 양이 어마어마하고 이를 효율적으로 다루는 것이 돈과 직결되기 때문에 데이터베이스를 관리할 미들웨어가 필요하게 됩니다. 또한 우리의 웹 서비스에서도 데이터는 체계적으로 관리되어야 합니다. 예를 들어 회원의 아이디, 비밀번호, 이름과 같은 정보를 일정한 형식에 맞추어 저장하고 편리하게 수정하거나 조회할 수 있어야겠죠. 데이터베이스를 관리하는 이러한 미들웨어를 데이터베이스 관리 시스템(DBMS: Database Management System)이라고 합니다. 

## Relational Database

그렇다면 관계형 데이터베이스(RDB : Relational Database)란 무엇일까요? 관계형 데이터베이스란 현재 가장 많이 사용되고 있는 데이터베이스의 한 종류입니다. 관계형 데이터베이스는 테이블(table)로 이루어져 있으며, 이 테이블은 키(key)와 값(value)의 관계를 나타냅니다. 이처럼 데이터의 종속성을 관계(relationship)로 표현하는 것이 관계형 데이터베이스의 특징입니다. 

관계형 데이터베이스의 테이블(table)은 다음 그림처럼 구성됩니다. 행과 열로 구성된 표라고 생각하시면 됩니다. 이 그림은 [TCPSchool](http://tcpschool.com/mysql/mysql_intro_relationalDB)에서 참고하였습니다.

![Imgur](https://i.imgur.com/yG6HvtW.png)

즉, 관계형 데이터베이스란 여러 개의 테이블이 서로 관계를 맺고 있는 형태의 데이터베이스입니다. 그렇다면 관계형 데이터베이스 말고 다른 형태의 데이터베이스도 있을까요? 오늘날 처리할 데이터가 기하급수적으로 늘어나면서 NoSQL이라는 새로운 형태가 부상하고 있습니다. 관계형 데이터베이스는 데이터들을 모두 2차원 행렬의 형태로 저장하기 때문에 확장성이 부족하다는 단점이 있었습니다. NoSQL은 대용량의 비정형 데이터를 처리하는데 강점이 있어 많은 주목을 받고 있습니다. NoSQL에 대해 더 궁금하신 분들은 [여기](https://www.upwork.com/hiring/data/sql-vs-nosql-databases-whats-the-difference/)를 참고하시면 좋을 것 같습니다.

## MySQL

다시 MySQL로 돌아와 보겠습니다. MySQL이란 관계형 데이터베이스를 효율적으로 관리하기 위한 미들웨어의 일종으로 널리 사용되고 있습니다. MySQL의 장점은 다음과 같습니다. MySQL은 오픈 소스 프로그램으로 무료로 사용할 수 있습니다. 다중 사용자와 다중 스레드를 지원합니다. 또한, C언어, C++, JAVA, PHP 등 여러 프로그래밍 언어를 위한 다양한 API를 제공하고 있습니다. MySQL은 유닉스, 리눅스, 윈도우 등 다양한 운영체제에서 사용할 수 있으며, 특히 PHP와 함께 웹 개발에 자주 사용됩니다. 또한 널리 알려진 표준 SQL 형식을 사용하고 있습니다.

## SQL

SQL(Structured Query Language)은 데이터베이스에서 데이터를 정의, 조작, 제어하기 위해 사용되는 언어이며, 각 목적에 맞게 세 가지로 구분할 수 있습니다. 

| 속성   | 설명                                       | 주요 명령어                           |
| ---- | ---------------------------------------- | -------------------------------- |
| DDL  | 데이터베이스나 테이블 등을 생성, 삭제하거나 그 구조를 변경하기 위한 명령어 | CREATE, ALTER, DROP              |
| DML  | 데이터베이스에 저장된 데이터를 처리하거나 조회, 검색하기 위한 명령어   | INSERT, UPDATE, DELETE, SELECT 등 |
| DCL  | 데이터베이스에 저장된 데이터를 관리하기 위하여 데이터의 보안성 및 무결성 등을 제어하기 위한 명령어 | GRANT, REVOKE 등                  |

그럼 이제 간단한 SQL 문법에 대해 알아보도록 하겠습니다.

### Database 생성, 삭제, 열람, 선택

테이블을 생성하기에 앞서 데이터터베이스를 생성, 삭제, 열람, 선택하기 위한 SQL 쿼리는 다음과 같습니다. 한글을 사용하기 위하여 생성부분에서 인코딩을 utf-8로 지정해 주었습니다.

```sql
CREATE DATABASE '데이터베이스명' CHARACTER SET utf-8 COLLATE utf8_general_ci;
```

```sql
DROP DATABASE '데이터베이스명';
```

```sql
SHOW DATABASES;
```

```sql
USE '데이터베이스명';
```

### Table 생성, 삭제, 열람

테이블은 데이터가 실질적으로 저장되는 저장소입니다. 먼저 테이블을 생성해 보겠습니다.

```
CREATE TABLE table_name (
    칼럼명1 data_type,
    칼럼명2 data_type
)
```

위와 같이 테이블 명을 지정해준 다음 괄호 안에 컬럼명과 데이터 타입을 지정해 주어야 합니다.

```
CREATE TABLE `student` (
    `id`  tinyint NOT NULL ,
    `name`  char(4) NOT NULL ,
    `sex`  enum('남자','여자') NOT NULL ,
    `address`  varchar(50) NOT NULL ,
    `birthday`  datetime NOT NULL ,
    PRIMARY KEY (`id`)
);
```

예시로 5개의 컬럼을 가진 student라는 테이블을 만드는 SQL 쿼리입니다. NOT NULL은 이 컬럼에 NULL값을 허용하지 않겠다는 의미입니다. 또한 마지막 줄에서는 id라는 컬럼을 이 테이블의 고유 키로 사용하고 있습니다. 고유 키는 이 테이블에서 데이터를 구분하기 위한 고유의 값이며 중복을 허용하지 않습니다.

테이블 리스트를 보여주고 테이블을 제거하기 위한 쿼리는 각각 다음과 같습니다.

```
SHOW tables;
```

```
DROP TABLE '테이블명'
```

### TABLE에 데이터를 삽입, 변경, 조회

만들어진 테이블에 실제 데이터를 삽입, 변경, 조회해 보겠습니다. 먼저 데이터를 삽입하는 SQL 쿼리는 **INSERT** 문입니다. 테이블 이름과 컬럼 이름을 지정해 주고 순서에 맞추어 삽입할 값을 넣어 주면 됩니다. 모든 컬럼의 값을 순서대로 넣어줄 경우 table_name 뒤의 (column1, column2, column3, ...) 부분은 생략할 수 있습니다. 

```
INSERT INTO table_name (column1, column2, column3,...) VALUES (value1, value2, value3,...)
```

앞에서 생성한 student 테이블에 id가 1이고 이름이 하둡인 새로운 데이터를 삽입해 보겠습니다.

```
INSERT INTO `student` (`id`, `name`, `sex`, `address`, `birthday`) VALUES ('1', '하둡', '남자', 'seoul', '2000-11-16');
```



다음으로 데이터를 수정하기 위한 **UPDATE** 문입니다. WHERE 조건에서 어떤 데이터를 수정할 것인지 지정합니다. 만약 지정하지 않으면 컬럼의 모든 값이 바뀌게 됩니다.

```
UPDATE 테이블명 SET 컬럼1=컬럼1의 값, 컬럼2=컬럼2의 값 WHERE 대상이 될 컬럼명=컬럼의 값
```

student 테이블에서 id가 1인 컬럼의 이름을 하둡이 아니라 스파크로 변경하려면 다음과 같습니다.

```
UPDATE `student` SET name='스파크' WHERE id=1;
```



데이터를 수정하기 위한 **DELETE**문입니다. DELETE문은 행단위로 데이터를 삭제하며 테이블 전체를 삭제하기 위해서는 DROP이나 TRUNCATE를 사용합니다. DROP은 테이블 전체를 삭제하는 반면 TRUNCATE는 테이블 안의 모든 값을 삭제하고 테이블의 형태는 남겨두게 됩니다. DELETE문의 WHERE 조건에서 어떤 데이터를 삭제할 것인지 지정합니다.

```
DELETE FROM 테이블명 [WHERE 삭제하려는 칼럼 명=값]
```

student 테이블에서 id가 1인 데이터를 삭제하려면 다음과 같습니다.

```
DELETE FROM `student` WHERE id = 1;
```



마지막으로 테이블에서 데이터를 조회하는 **SELECT**문입니다. SQL에서 가장 자주 사용되며 많은 옵션이 있기 때문에 자세한 내용은 [생활코딩의 SQL 강의](https://opentutorials.org/course/195/1403)를 참고해 주세요. 여기에서는 간단히 소개하도록 하겠습니다. 

```
SELECT 칼럼명1, 칼럼명2 
    [FROM 테이블명 ]
    [WHERE 조건]
    [ORDER BY 칼럼명 [ASC | DESC]] 
    [LIMIT offset, 조회 할 행의 수]
```

ORDER BY는 지정한 컬럼에 대해 전체 데이터를 정렬해줍니다. ASC는 오름차순, DESC는 내림차순입니다. LIMIT로 조회할 행의 수를 제한할 수 있습니다.  앞서 만든 student 테이블에서 다양한 방식으로 데이터를 조회해 보겠습니다.

1. student 테이블의 모든 데이터를 조회

```
SELECT * FROM student;
```

2. student 테이블의 name과 birthday 컬럼만 조회

```
SELECT name, birthday FROM student;
```

3. student 테이블에서 id가 1인 데이터를 조회

```
SELECT * FROM student WHERE id=3;
```

4. student 테이블에서 성이 남자인 테이터를 2개만 조회

```
SELECT * FROM student WHERE sex='남자' LIMIT 2;
```





[http://exert.tistory.com/entry/MySQL이란](http://exert.tistory.com/entry/MySQL%EC%9D%B4%EB%9E%80)

http://tcpschool.com/mysql/DB

https://opentutorials.org/course/195

