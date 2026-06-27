# B5-1 : SQL로 만드는 나만의 데이터베이스
- 테이블 설계 부터 요구사항을 쿼리로 작성하는 흐름

## 핵심 목표
- 데이터베이스가 “엑셀과 뭐가 다른지”, 왜 테이블로 나눠 저장하는지 설명할 수 있다.
- PK/FK가 무엇이고, 1:N 관계가 데이터를 어떻게 연결하는지 말로 설명할 수 있다.
- SELECT / INSERT / UPDATE / DELETE를 언제 쓰는지 구분할 수 있다.
- JOIN과 GROUP BY로 “연결된 데이터를 한 번에 뽑는 방법”을 설명할 수 있다.
- 실무에서 흔한 요구(검색/정렬/집계/랭킹)를 SQL로 어떻게 풀지 감을 잡을 수 있다.
- 인덱스가 왜 필요한지, 어떤 컬럼에 적용하면 좋은지 기초적인 이해를 할 수 있다.


## 결과물
1. 스키마 생성 SQL: `docs/sql/schema.sql`
2. 샘플 데이터 INSERT SQL: `docs/sql/data.sql`
3. 쿼리 15개 SQL: `docs/sql/query.sql`
4. 실행 결과 캡처 폴더: `docs/screenshot/`
5. (선택) ERD 다이어그램 이미지 1개 (draw.io, dbdiagram.io 등 활용)


## 요구사항
1. DB 환경 준비 (MySQL로 선택)
- 설치
- 실행 도구 (DBeaver)

2. 데이터 모델 (스키마) 설계
- 최소 4개 테이블 설계
- PK 와 최소 2개 이상의 FK 를 이용한 1: N 관계
- 주제는 직접 선정

3. 제약 조건 적용
- 최소 1개 컬럼에 NOT NULL 적용
- 최소 1개 컬럼에 UNIQUE 적용
- FK 가 없는 값을 참조하지 않아야 한다.

4. 샘플 데이터 준비
- 각 테이블에 최소 10행 이상의 데이터 입력
- FK 로 연결된 데이터가 실제로 관계를 갖도록 입력

5. 핵심 SQL 쿼리 15개 작성
- 기본 조회 4개 이상 (WHERE, ORDER BY, LIMIT 포함)
- 조인 4개 이상 (INNER JOIN 2개 이상, LEFT JOIN 1개 이상 포함)
- 집계 3개 이상 (COUNT, SUM, AVG 중 2개 이상 + GROUP BY)
- 서브쿼리 1개 이상
- 데이터 수정 및 삭제 2개 이상 (UPDATE, DELETE)
- 인덱스 1개 이상 (CREATE INDEX + 적용 이유 1줄)

<br>
<br>

# 실행 순서
1. MySQL 접속 후 DB 생성 및 선택
   ```sql
   CREATE DATABASE codyssey_mission_db;
   USE codyssey_mission_db;
   ```

2. 스키마 생성
   ```sql
   SOURCE docs/sql/schema.sql;
   ```

3. 샘플 데이터 삽입
   ```sql
   SOURCE docs/sql/data.sql;
   ```

4. 쿼리 실행
   ```sql
   SOURCE docs/sql/query.sql;
   ```

<br>
<br>

# 과제 수행 내역
리눅스 Ubuntu/Debian 계열 기준
## 1. MySQL 설치
1. 설치
    ```bash
    sudo apt update
    sudo apt install mysql-server
    ```

2. 서비스 시작
    ```bash
    sudo service mysql start

    # 또는
    sudo systemctl start mysql
    ```

3. 서비스 상태 확인
    ```bash
    sudo systemctl status mysql
    ```
    ![alt text](docs/screenshot/b5-1_mysql_started.png)

## 2. MySQL 접속
1. 로그인
    ```bash
    mysql -u root -p
    # 이후 비밀번호 입력
    ```

2. DB 목록확인
    ```sql
    SHOW DATABASES;
    ```

## 3. DB 생성
1. DB 생성
    ```sql
    CREATE DATABASE <DB이름>;
    ```

2. DB 선택(사용)
    ```sql
    USE <DB이름>;
    ```

3. 기타 - DB 삭제
    ```sql
    DROP DATABASE <DB이름>;
    ```


## 4. TABLE 생성
### 테이블 설계
주제를 Codyssey 미션관리 로 잡고, 학생–미션–진도–동료평가를 관리하는 데이터베이스로 설계했다.

1. 학생 정보 (student)
- id, 이름, 이메일, 과정, 가입일
2. 미션 정보 (mission)
- id, 미션 제목, 카테고리, 난이도, 예상 소요시간, 미션 시작일
3. 진도 관리 (mission_progress)
- id, 학생 id, 미션 id, 진행 상태, 미션 제출일, 수정일, 최종 결과
4. 동료 평가 (peer_review)
- id, 평가자 id, 피평가자 id, 평가 결과 (PASS / FAIL), 코멘트, 작성일

### 테이블 목록 확인
```SQL
SHOW TABLES;
```

### 각 테이블 구조 확인
```SQL
DESC <테이블명>;
```

