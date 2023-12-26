# 실행계획

#### 실행계획
- 사용자가 SQL을 실행하여 데이터를 추출하려고 할 때, 옵티아미저가 수립하는 작업절차
### 옵티아미저 동작 순서
1. SQL 해석
2. 실행계획 수립
3. 실행
#### 실행계획 확인 방법 (SQL)
1. EXPLAIN PLAN
 - SQL에 대한 실행계획만을 확인할 수 있음
 - 명령을 사용할 때 데이터를 처리하지 않음
```SQL
EXPLAIN PLAN
SET STATEMENT_ID = 'TEST1' INTO PLAN_TABLE
FOR 
SELECT E.ENAME, E.DEPNO, D.DNAME
FROM EMP E, DEPT D
WHERE E.DEPTNO = D.DEPTNO;
```
 
 
2. SET AUTOTRACE
 - EXPLAIN PLAN 명령과는 달리 한 번의 명령으로, 여러개의 SQL에 대한 실행계획을 바로 볼 수 있음
 - 다양하게 옵션을 사용할 수 있어서 여러 가지의 정보를 선택적으로 확인할 수 있음
```SQL
SET AUTOTRACE ON;
SELECT E.ENAME, E.DEPNO, D.DNAME
FROM EMP E, DEPT D
WHERE E.DEPTNO = D.DEPTNO
```
 - SET AUTOTRACE 옵션
```SQL
SET AUTOTRACE ON EXPLAIN; 
SET AUTOTRACE ON STATISTICS; 
SET AUTOTRACE TRACEONLY; 
SET AUTOTRACE TRACEONLY EXPLAIN; 
SET AUTOTRACE TRACEONLY STATISTICS; 
SET AUTOTRACE OFF; 
```

# 옵티마이저
### 옵티마이저
- 사용자가 실행한 SQL을 해석하고, 데이터를 추출을 위한 실행계획을 수립하는 프로세스
- 사용되는 옵티마이저 종류에 따라 실행계획이 다르게 수립될 수 있
### 옵티마이저 종류
1. RBO
 - 기본적으로 15개의 순위가 매겨진 규칙이 있음
 - SQL에 대한 실행계획이 하나 이상일 경우에 순위가 높은 규칙을 이용함
 - 수립될 실행계획이 예측 가능하기 때문에 개발자가 원하는 처리 경로로 유도하기가 쉬움
```SQL
1. ROWID에 의한 1ROW
2. 클러스터 조인에 의한 1ROW
3. UNIQUE나 PRIMARY KEY를 사용한 해시클러스터 키에 의한 1ROW
4. UNIQUE나 PRIMARY KEY에 의한 1ROW
5. 클러스터 조인
6. 해시 클러스터 조인
7. 클러스터 키
8. 결합 칼럼 인덱스
9. 단일 컬럼 인덱스
10. 인덱스에 의한 유한 영역 검색
11. 인덱스에 의한 무한 영역 검색
12. SORT MERGE 조인
13. 인덱스로 구성된 컬럼의 최대 또는 최소
14. 인덱스로 구성된 컬럼으로 ORDER BY
15. FULL TABLE SCAN
```
2. CBO
 - 대상 ROW들을 처리하는데 필요한 자원 사용을 최소화해서 궁극적으로 데이터를 빨리 처리하는데 목적이 있음
 - CBO에 영향을 미치는 비용 산정 요소 : 각종 통계 정보, HINT, 연산자, 인덱스 클러스터, DBMS 버전, CPU/MEMORY 용량, DISK I/O
 - CBO의 비용산정에 사용되는 통계정보를 생성하기 위해 정기적으로 ANALYZE 작업이 필요함
 ```SQL
ANALYZE TABLE EMP COMPUTE STATISTICS;
ANALYZE TABLE EMP ESTIMATE STATISTICS SAMPLE 10 PERCENT;
ANALYZE TABLE EMP ESTIMATE STATISTICS SAMPLE 5 ROWS;
```



