### NESTED LOOPS JOIN
1. Driving Table(기준 테이블), Driven Table(연결되는 테이블)로 나뉨
2. Driven Table의 연결컬럼은 인덱스가 설정되어 있어야함
```SQL
SELECT A.COLOR, B.SIZE
FROM TABLE_A AS A, TABLE_B AS B
WHERE A.JOINKEY_A = B.JOINKEY_B
AND A.COLOR = 'RED'
AND B.SIZE = 'MED';
```
3. A 테이블에 COLOR에 대한 인덱스가 있다면 우선 COLOR 인덱스를 통해 A 테이블 데이터를 조회함
4. B 테이블에서 JOINKEY_B 컬럼 인덱스로 데이터를 조회함
5. B 테이블에서 SIZE가 MED인 값만 추출함
6. A 테이블의 조회된 건수에 따라 연결 횟수가 결정됨 (조회된 A 테이블의 건수가 백만건이라면 백만번의 조인이 수행됨)

### NESTED LOOPS JOIN 장단점
1. 인덱스에 의한 랜덤 액세스에 기반하고 있기 때문에 대량의 데이터 처리 시 적합하지 않음
2. Driving Table로는 테이블의 데이터가 적은 마스터 테이블이거나, where절 조건으로 적절하게 row를 제어할 수 있는 것이어야함 (Driving Table 건수가 연결 횟수를 결정하기 때문)
3. Driven Table에는 조인을 위한 적절한 인덱스(연결컬럼)가 생성되어 있어야함

### 조인 순서 제어 방법
1. 조인 순서 제어를 위한 힌트 사용
```SQL
/*+ORDERED*/
/*+LEADING(TABLE명)*/
```
2. VIEW 활용
3. SUPPRESSING 활용
4. FROM 절의 테이블 순서 변경
   - RBO 하에서 각 테이블에 대한 규칙이 동일할 때 FROM 절로 부터 멀리 있는 테이블부터 처리함
   - CBO에서는 이 방법은 의미가 없음

### 연결고리에 대한 인덱스
1. A 테이블에는 연결고리컬럼에 인덱스가 있고 B 테이블에는 인덱스가 없다면 B 테이블을 DRIVNG TABLE로 설정하여 한번만 FULL SCAN을 수행하고 조인 시에는 A 테이블의 인덱스를 사용하도록 해야함
2. A, B 테이블 모두 연결고리 컬럼에 인덱스가 없다면 SORT, MERGE JOIN을 사용하여 조인을 수행해야함

### 문제
- 문제점 발견 및 개선하기
![image](https://github.com/HyeokChan/Obsidian/assets/48059565/0312803c-b2c1-440c-9159-81cc916a1800)
![image](https://github.com/HyeokChan/Obsidian/assets/48059565/cd180854-d870-4d19-9843-faa07d13d900)
- PK로 봤을 때 데이터 양이 A < B < C 순으로 많음
- 데이터 양이 적은 테이블부터 DRIVING TABLE로 사용이 되야함

```SQL
WHERE A.COURSE_CODE = B.COURSE_CODE
AND B.COURSE_CODE = C.COURSE_CODE
AND B.EXAM_NO = C.EXAM_NO
AND A.COURSE_CODE = '14';
```
- 조인 WHERE 절을 수정하여 개선 완료

---
### SORT/MERGE JOIN
- 연결고리에 인덱스가 전혀 없는 경우
- 대용량의 자료를 조인해야 함으로써 인덱스 사용에 따른 랜덤 액세스의 오버헤드가 많음 경우
### SORT/MERGE JOIN 수행 순서
1. 각 테이블에 대해 동시에 독립적으로 데이터를 먼저 읽어 들임
2. 읽혀진 각 테이블의 데이터를 조인을 위한 연결고리에 대하여 정렬을 수행함
3. 정렬이 모두 끝난 후에 조인 작업이 수행됨
### SORT/MERGE JOIN 튜닝 포인트
- 각 테이블로 부터 데이터를 빨리 읽어 들이도록 함
- 메모리(SORT_AREA_SIZE)를 최적화 함

### 성능 상 불리한 경우
- A, B 테이블에서 데이터를 각각 조회하고 정렬을 수행할 때 A, B 테이블의 데이터가 차이가 많이 나는 경우 (A<B) A 테이블 정렬 이후에 B 테이블이 정렬될 때까지 대기 상태로 유지됨

### SORT/MERGE JOIN 장단점
1. 연결고리에 인덱스가 생성되어 있지 않은 경우에 빠른 조인을 위하여 사용됨
2. 조인하고자 하는 각 테이블에 대해서 독립적으로 데이터를 읽어 들일 때, 이를 얼마나 빠르게 할 것인가가 중요함
3. 각 테이블로부터 읽혀진 데이터를 연결고리에 대해 정렬을 수행할 때 이를 얼마나 빠르게 할 것인가가 중요함

---
### HASH JOIN
1. NESTED LOOPS JOIN : 인덱스 사용에 의한 랜덤 액세스의 오버헤드
2. SORT/MERGE JOIN : 정렬 작업으로 인한 오버헤드
3. 각 문제 해결을 위해 HASH JOIN 사용
4. SORT/MERGE 조인과 비교해보면, 각 테이블에 대한 처리를 독립적으로 하는 것은 같지만 HASH JOIN에서는 DRIVING TABLE이 있음
5. 읽어들인 각 테이블의 데이터를 서로 조인하기 위해 해싱을 이용해서 해시 값을 만듬
6. 해시 값으로 조인을 수행함

### HASH JOIN 튜닝 포인트
- DRIVING TABLE 결정
- 각 테이블로부터 데이터를 읽어 들일 때, 빨리 읽을 수 있도록 함
- 메모리(HASH_AREA_SIZE)를 최적화함

### HASH JOIN 수행 절차
1. 옵티마이저가 DRIVING 테이블을 선택함
2. DRIVING 테이블에 해싱을 수행하여 해시값을 생성함
3. DRIVEN 테이블에도 같은 해싱을 수행하여 해시값을 생성함
4. 각각의 DRIVING, DRIVEN 테이블에 해시값 충돌(원 데이터는 다른데 해시값은 같은 경우)을 방지하기 위해 다시 해싱을 수햄함
5. 해시값으로 조인을 처리함

### HASH JOIN 장단점
- HASH BUCKET이 조인 집합에 구성되어 해시 함수 결과를 저장해야 하는데 이러한 처리에는 많은 메모리와 CPU 자원을 소모하게 됨
- 하드웨어 자원이 넉넉한 상황에서는 다른 조인에 비해 효율적이지만, 부족한 상황에서는 다른 조인 방법보다 오히려 느려질 수도 있음

---

### 조인조건이 없는 조인
### CARTESIAN PRODUCT의 개념
1. WHERE절이 없는 조인 수행
2. 조인을 위한 조건 없이 조인 수행
3. 데이터 복제라는 개념을 활용하기 위해 사용하지만 잘못 사용하면 데이터를 부풀리는 결과만 낳게

### CARTESIAN PRODUCT 적용 예제
1. UNION ALL 대체
```SQL
SELECT '직군별' AS CLASS, JOB, COUNT(*) AS CNT
FROM EMP
GROUP BY JOB
UNION ALL
SELECT '부서별' AS CLASS, TO_CHAR(DEPTNO), COUNT(*) AS CNT
FROM EMP
GROUP BY DEPTNO
UNION ALL
SELECT '총인원' AS CLASS, NULL, COUNT(*) AS CNT
FROM EMP
```
- UNION ALL 대신에 CARTESIAN PRODUCT를 이용해서 조회
- EMP 테이블에서는 데이터를 한번만 읽도록 개선
```SQL
SELECT DECODE(RN,1,'직군별',2,'부서별','총인원') AS CLASS
DECODE(RN,1,JOB,2,DEPTNO)
SUM(CNT)
FROM (SELECT JOB, DEPTNO, COUNT(*) AS CNT
	 FROM EMP
	 GROUP BY JOB, DEPTNO),
	 (SELECT ROWNUM AS RN
	 FROM (SELECT LEVEL FROM DUAL CONNECT BY ROWNUM <= 3))
GROUP BY RN,
DECODE(RN,1,'직군별',2,'부서별','총인원'),
DECODE(RN,1,JOB,2,DEPTNO);
```

2. 데이터 구조 변환
![image](https://github.com/HyeokChan/Obsidian/assets/48059565/f3f5192a-74d0-4422-a170-d4c46cb48ede)
```SQL
SELECT A.ENAME, B.QTR,
DECODE(B.QTR,1,A.Q1,2,A.Q2,3,A.Q3,A.Q4) AS SL
FROM (SELECT ENAME,Q1,Q2,Q3,Q4,ROWNUM
	 FROM EMP_SAL) A
	 (SELECT ROWNUM AS ATR
	 FROM (SELECT LEVEL FROM DUAL CONNECT BY ROWNUM <= 4)) B
ORDER BY 1, 2;	 
```
- (참고) 11G 버전 부터 UNPIVOT 함수를 사용해서 구조 변환도 가능함
```SQL
WITH MYTAB AS (
SELECT ENAME, Q1, Q2, Q3, Q4
FROM EMP_SAL)
SELECT ENAME, GRP AS QTR, NO
FROM MYTAB
UNPIVOT (NO FOR GRP IN (Q1 AS 1, Q2 AS 2, Q3 AS 3, Q4 AS 4))
ORDER BY ENAME;
```
3. 카티션 프로덕트를 통해 1년치 모든 날짜를 조회하는 쿼리 등도 쉽게 구현할 수 있음

----
