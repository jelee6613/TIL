

# 01_Database_Basic

* 데이터베이스는 체계화된 데이터의 모임
* 몇 개의 자료 파일을 조직적으로 통합
* 자료 항목의 중복을 없애고, 자료를 구조화하여 기억시켜 놓은 자료의 집합체
* 파일❌이 아닌  소프트웨어 ✔



## RDB

관계형 데이터베이스

키와 값들의 간단한 관계를 표 형태로 정리한 데이터베이스

* 스키마: 데이터베이스에서 자료의 구조, 표현방법, 관계등 전반적인 명세를 기술한 것
* 테이블: 열(컬럼/필드)과 행(레코드/값)의 모델을 사용해 조직된 데이터 요소들의 집합



## RDMBS

관계형 데이터베이스 관리 시스템 (Relational Database Management System)

관계형 모델을 기반으로 하는 데이터베이스 관리시스템을 의미

* MySQL
* SQLite (서버 형태❌ 파일 형식✔ 응용 프로그램에 넣어서 사용하는 가벼운 DB)
* PostgreSQL
* ORACLE
* MS SQL



## SQL

* Structured Query Language
* **RDMBS**의 **데이터 관리**를 위해 설계된 특수 목적 프로그래밍 언어
* 데이터베이스 스키마 생성 및 수정
* 자료의 검색 및 관리
* 데이터베이스 객체 접근 조정 관리



### Data Type

1. NULL
2. INTEGER
3. REAL
4. TEXT
5. BLOB



### 분류

* DDL - 데이터 정의 언어 (테이블) `CREATE`, `DROP`, `ALTER`

* DML - 데이터 조작 언어 (레코드) `INSERT`, `SELECT`, `UPDATE`, `DELETE` (CRUD)

* DCL - 데이터 제어 언어





---



`CREATE` -  **테이블 생성**

```sqlite
CREATE TABLE classmates (
    id INTEGER PRIMARY KEY AUTOINCREMENT, (default는 rowid, NOT NULL)
    name TEXT NOT NULL,
    age INT,
    address TEXT
);
```

`NOT NULL` : 유/무에 따라 필수값 설정 가능( 단, pk는 NOT NULL이 기본)

`AUTOINCREMENT` : 레코드 추가할 때 삭제된 id 값을 재사용하지 않고 다음 id 값 사용

---



`INSERT` - **단일 행 삽입**

```sqlite
#1 INSERT INTO classmates VALUES('홍길동', 24, '서울');
#2 INSERT INTO classmates (name, age, address) VALUES ('홍길동', 24, '서울');
#3 INSERT INTO classmates VALUES(1, '홍길동', 24, '서울');
```

---



`SELECT` - READ

* `LIMIT` - 몇개까지? `SELECT 컬럼1, 컬럼2 FROM 테이블이름 LIMIT 2 OFFSET 3;`
* `WHERE` - 검색 조건 `SELECT name FROM classmates WHERE address='서울';`
* `SELECT DISTINCT` - 중복 행 제거

```sqlite
#전체조회 SELECT * FROM classmates;
#특정열조회 SELECT name FROM classmates;
```

---



`DELETE`

```sqlite
DELETE FROM classmates WHERE rowid=2;
```

classmates 테이블에 id가 5인 레코드 삭제

---



`UPDATE`

```sqlite
UPDATE 테이블이름 SET name='오바마', address='제주도' WHERE rowid=2;
```



### csv

```sqlite
sqlite> .mode csv
sqlite> .import users.csv 테이블이름
```



### Aggregate Functions

* `COUNT` : 그룹의 항목 수를 가져옴
* `AVG` : 모든 값의 평균을 계산
* `MAX` : 그룹에 있는 모든 값의 최대값을 가져옴
* `MIN` : 그룹에 있는 모든 값의 최소값을 가져옴
* `SUM` : 모든 값의 합을 계산



### LIKE operator

패턴 일치를 기반으로 데이터를 조회하는 방법



#### wildcards

* % (percent sign) : 이 자리에 문자열이 있을 수도, 없을 수도 있다.
* _ (underscore) : 반드시 이 자리에 한 개의 문자가 존재해야 한다.



### ORDER BY

* 조회 결과 집합을 정렬
* SELECT 문에 추가하여 사용
* ASC : 오름차순(default) / DESC : 내림차순



Q. classmates에서 나이 순으로 오름차순 정렬하여 상위 10개만 조회한다면?

```sqlite
SELECT * FROM classmates ORDER BY age ASC LIMIT 10;
```



### GROUP BY

* 행 집합에서 요약 행 집합을 만듦
* WHERE 절이 있을 경우 반드시 WHERE 절 뒤에 작성



Q. users에서 각 성(last_name)씨가 몇 명씩 있는지 조회한다면?

```sqlite
SELECT last_name, COUNT(*) (AS name_count) FROM users GROUP BY last_name; 
```

`AS name_count` 를 작성하면 `COUNT`에 해당하는 컬럼 명을 바꿔서 조회 가능





### ALTER TABLE

1. table 이름 변경
2. 테이블에 새로운 column 추가
3. column 이름 수정

```sqlite
#1 ALTER TABLE 기존테이블이름 RENAME TO 새로운테이블이름;
#2 ALTER TABLE 테이블이름 ADD COLUMN 컬럼이름 데이터타입설정;
#2-1 ALTER TABLE 테이블이름 ADD COLUMN 컬럼이름 TEXT NOT NULL DEFAULT '내용';
#2-2 ALTER TABLE 테이블이름 ADD COLUMN 컬럼이름 TEXT;
```



**#2** 새로운 column 추가하면 기존 레코드의 정보가 없으므로 `NOT NULL`을 작성하지 말거나,
 `default` 값을 지정해 줘야 한다.
