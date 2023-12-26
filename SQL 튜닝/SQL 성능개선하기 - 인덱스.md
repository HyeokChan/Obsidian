# 인덱스
### 인덱스의 필요성
- 데이터베이스에 저장된 자료를 더욱 빠르게 조회하기 위해 인덱스를 생성하여 사용함
- 일반적으로 10~15% 이하의 데이터를 처리하는 경우에 효율적, 그 이상의 데이터를 처리할 땐 인덱스를 사용하지 않는 것이 더 나음
### B\*TREE 구조
- 인덱스의 데이터 저장 방식
- ROOT, BRANCH, LEAF NODE로 구성
  
![Pasted image 20231226153522](https://github.com/HyeokChan/Obsidian/assets/48059565/ad98337c-e33c-4df8-a6f8-c22776bca975)

- B\*TREE 구조의 핵심은 SORT
1. 인덱스를 사용하면 ORDER BY에 의한 SORT를 피할 수 있음
2. MAX/MIN의 효율적인 처리가 가능함

### 인덱스 활용 예시
- (COURSE_CODE, YEAR, COURSE_SQ_NO)로 구성된 인덱스 EC_COURSE_SQ_PK가 있음
```SQL
SELECT COURSE_CODE, YEAR, COURSE_SQ_NO
FROM EC_COURSE_SQ
WHERE COURSE_CODE = 1960
AND YEAR = '2022'
ORDER BY COURSE_SQ_NO DESC
```
```SQL
SELECT MAX(COURSE_SE_NO)
FROM EC_COURSE_SQ
WHERE COURSE_CODE = 1960
AND YEAR = '2022'
```
- COURSE_SQ_NO 컬럼으로 ORDER BY를 하였지만 PK의 나머지 구성요소인 COURSE_CODE, YEAR를 조건문으로 사용하고 있어서 인덱스를 사용하여 COURSE_SQ_NO에 의한 SORTING을 피할 수 있음
- MAX/MIN도 동일
- 인덱스를 구성하지 않았으면 조건절에 의한 데이터를 구한 뒤 그 데이터를 SORTING 하는 작업이 필요함

### 인덱스 선정 절차
1. 프로그램 개발에 이용된 모든 테이블에 대하여 ACCESS PATH 조사
2. 인덱스 컬럼 선정 및 분포도 조사
3. CRITICAL ACCESS PATH 결정 및 우선 순위 선정
4. 인덱스 컬럼의 조합 및 순서 결정
5. 시험 생성 및 테스트
6. 결정된 인덱스를 기준으로 프로그램 반영
7. 실제 적용

### 인덱스 생성 및 변경 시 고려할 사항
- 기존 프로그램의 동작에 영향성 검토
- 필요할 때마다 인덱스 생성으로 인한 인덱스 개수의 증가와 이로 인한 DML 작업의 속도
- 비록 개별 컬럼의 분포도가 좋지 않을지라도 다른 컬럼과 결합하여 자주 사용되고, 결합할 경우 분포도가 양호하다면 결합 인덱스 생성을 긍정적으로 검토

### 인덱스 스캔의 원리
- 옵티마이저가 인덱스 사용을 위한 실행계획 수립
1. 조건을 만족하는 최초의 인덱스 ROW를 찾음(인덱스 테이블)
2. ACCESS된 인덱스 ROW의 ROWID를 이용해서 테이블에 있는 있는 ROW를 찾음(RANDOM ACCESS) 
3. 처리 범위가 끝날 때까지 차례대로 찾음
- 인덱스 스캔 시에는 한번의 I/O가 발생할 때 마다 한 개의 BLOCK씩을 처리함

### 문제
- 문제점 발견 및 개선하기
  
![Pasted image 20231226154906](https://github.com/HyeokChan/Obsidian/assets/48059565/198d927f-1d51-433f-90cb-545b0992d1bc)

- MIN, MAX를 동시에 구하여 인덱스를 사용할 수 있음에도 실행계획에 SORTING이 발생함
  
![Pasted image 20231226155131](https://github.com/HyeokChan/Obsidian/assets/48059565/efb95e33-45e3-4b2e-a47c-374119cf2902)

```SQL
WHERE A.COURSE_SQ_NO AS MAX_SQ FROM EC_COURSE_SQ A WHERE A.COURSE_CODE = 1960 AND A.YEAR = '2002' AND ROWNUM = 1
```
- MIN, MAX를 분리해서 구하고 UNION ALL을 사용하여 각각의 값을 구할 때 인덱스를 활용할 수 있도록 개선

---
# 결합인덱스
### 인덱스 머지
- 한 테이블에 여러 컬럼에 대한 개별 인덱스가 있을 때 각각의 인덱스가 하나씩 처리됨
### 결합인덱스
- 여러 컬럼으로 하나의 인덱스를 구성해서 인덱스 머지보다 효율적으로 탐색이 가능함
### 결합인덱스 구성
- 조건절에서 AND 조건으로 자주 결합되어 사용되면서 결합했을 때 분포도가 좋은 컬럼들
- 다른 테이블과 조인의 연결고리로 자주 사용되는 컬럼들
- 하나 이상의 키 컬럼 조건으로 같은 테이블의 컬럼들이 자주 조회될 때
### 결합인덱스의 컬럼 순서 결정 방법
- 조건절에서 많이 사용되는 컬럼 우선
- EQUAL로 사용되는 컬럼 우선
- 분포도가 좋은 컬럼 우선
- 자주 이용되는 SORT 대상 컬럼의 순서로 결정

### 결합인덱스 컬럼에 대한 '='의 의미
```SQL
WHERE 시 LIKE '서%' 
AND 구 = '강남구' -- 체크조건
AND 동 = '역삼동' -- 체크조건

WHERE 시 = '서울시' -- 범위제한조건
AND 구 LIKE '강%'
AND 동 = '역삼동' -- 체크조건

WHERE 시 = '서울시' -- 범위제한조건
AND 동 = '역삼동' -- 범위제한조건
```
- LIKE조건 유무에 따라 범위제한조건, 체크조건으로 구분될 수 있음
- 범위제한조건으로 EQUAL이 사용될 때 성능이 좋음
### 인덱스 매칭률 향상을 통한 튜닝 예시
- EMP_PAY_X1 : (급여연월, 급여코드, 사원번호)
- 튜닝 전 : 매칭률 0/3
```SQL
WHERE 급여연월 LIKE '2016%'
AND 급여코드 = '정기급여' -- 앞의 LIKE 조건으로 인해 체크조건으로 EQUAL이 사용됨
```
- 튜닝 후 : 매칭률 2/3
```SQL
WHERE 급여연월 IN ('201601','201602','201603','201604','201605','201606','201607','201608','201609','201610','201611','201612') -- 범위제한조건
AND 급여코드 = '정기급여' -- 앞의 조건을 IN으로 변경하여 범위제한조건으로 사용됨
```

### 문제
- 문제점 발견 및 개선
![Pasted image 20231226230135](https://github.com/HyeokChan/Obsidian/assets/48059565/36f51b86-49e3-448c-a568-7ada162ecb5e)
- COURSE_CODE의 '<' 조건으로 인해 YEAR '=' 조건이 체크조건으로 사용됨, 매칭률 0/7
![Pasted image 20231226230427](https://github.com/HyeokChan/Obsidian/assets/48059565/0cb7f586-1bb0-43c3-bbe7-0a4481bae058)
```SQL
WHERE A.COURSE_CODE = B.COURSE_CODE
AND B.COURSE_CODE < 1000
AND A.YEAR = '2000'
GROUP BY A.COURSE_CODE;
```
- COURSE_CODE를 조인조건으로 사용하고 YEAR을 '=' 조건으로 사용하여 매칭률 2/7로 성능 개선
---
# 인덱스 활용이 불가능한 경우
### 인덱스를 사용하지 말아야 하는 경우
- 인덱스를 사용하면 한번의 I/0에 하나의 BLOCK만 읽어드릴 수 있다.
- 데이터 분포도가 15% 이상인 경우에는 FULL TABLE SCAN을 통해 한번의 I/O로 여러 BLOCK을 한번에 읽어드리는 것이 효과적이다.
### 인덱스 사용이 불가능한 연산자
1. NOT 연산자
 - 정렬된 인덱스 테이블에 특정 값에 NOT 연산자를 사용하면 분포도가 15% 이상이 되게 됨
2. IS NULL, IS NOT NULL 연산자
 - 인덱스 테이블에는 NULL값을 관리하지 않음
3. 옵티마이저의 취사 선택
 - 옵타마이저의 자의적 판단을 방지하고자 한다면 강제로 제어하기 위해 HINT 사용
4. EXTERNAL SUPPRESSING
 - 인덱스 컬럼에 변형을 가하면 인덱스로 활용할 수 없음
 - 불필요한 함수를 사용한 경우
 ```SQL
WHERE SUBSTR(ENAME,1,1) = 'M';
-- =>
WHERE ENAME LIKE 'M%';
```
- 문자열 결합
```SQL
WHERE JOB||DEPNO = 'MANAGER10';
-- =>
WHERE JOB = 'MANAGER' AND DEPTNO = 10;
```
- DATE 변수의 가공
```SQL
WHERE TO_CHAR(HIREDATE, 'YYYYMMDD') = '20021016';
-- =>
WHERE HIREDATE BETWEEN TO_DATE('20021016', 'YYYYMMDD') 
AND TO_DATE('20021016', 'YYYYMMDD') + INTERVAL '1' DAY - INTERVAL '1' SECOND;
```
- 산술식의 적용
```SQL
WHERE SAL*12 > 40000;
-- =>
WHERE SAL > 40000/12;
```
5. INTERNAL SUPPRESSING
- DBMS 내에서 자동 형변환으로 인해 데이터에 변환이 일어나는 경우
- 연산자체는 정상적으로 동작하나, 인덱스 사용이 불가능함
- 간단한 연산식
```SQL
COMM + '500';
```
- 논리비교 연산식
```SQL
BONUS > SAL / '10';
```
- 함수 호출
```SQL
MOD(SAL, '100');
```
### 옵티마이저에 의한 인덱스 선택 절차
- SALES 테이블 인덱스
1. IX1_SALES : 부서 + 기준일자
2. IX2_SALES : 품목
```SQL
SELECT *
FROM SALES
WHERE 부서 = '843'
AND 기준일자 = '970518'
AND 품목 = 'B023';
```
- 인덱스 매칭률이 IX1이 더 높으므로 IX1을 인덱스로 먼저 사용함
- IX1에 순번이라는 컬럼이 추가된다면 인덱스 매칭률이 IX2가 더 높아지므로 IX2를 인덱스로 먼저 사용함
- 인덱스 별 매칭률이 같다면 인덱스를 구성하는 컬럼의 개수가 많은 것을 우선적으로 선택함
- 인덱스 별 매칭률, 컬럼 개수가 모두 동일하다면 가장 최근에 생성된 인덱스를 우선적으로 선택함

### RBO, CBO가 선택한 인덱스 차이
- 인덱스 현황
1. EC_COURSE_SQ_PK : COURSE_CODE + YEAR + COURSE_SQ_NO
2. EC_COURSE_SQ_IDX_01 : YEAR (NON UNIQUE)
```SQL
SELECT MIN(COURSE_SQ_NO) AS MIN_SQ,
MAX(COURSE_SQ_NO) AS MAX_SQ
FROM EC_COURSE_SQ
WHERE COURSE_CODE = 1960
AND YEAR = '2002';
```
- RBO 옵티마이저는 매칭률이 높은 EC_COURSE_SQ_IDX_01 인덱스를 사용함
- CBO 옵티마이저는 범위를 더 좁힐 수 있는 EC_COURSE_SQ_PK 인덱스를 사용함

### 문제
- 문제점 발견 및 개선
![Pasted image 20231226235118](https://github.com/HyeokChan/Obsidian/assets/48059565/a2f9cb12-3b78-446a-a26a-67a7d5a5e75f)
- 결과행 138883 수가 15%를 증가하여 인덱스 사용을 안하는 것이 좋음
- 연도별 DECODE 처리를 하기 전에 GROUP BY를 먼저 사용하여 처리대상 데이터를 줄이는 것이 효율적

![Pasted image 20231226235130](https://github.com/HyeokChan/Obsidian/assets/48059565/d02072f6-7eff-4c8f-9ec2-38854ae19a2f)
```SQL
SELECT /*+FULL(EC_APPLY) */
COURSE_CODE, YEAR, SUM(DEPOSIT_AMOUNT) DEPOSIT_AMOUNT
FROM EC_APPLY
WHERE COURSE_CODE < 1000
AND YEAR BETWEEN '1999' AND '2002'
GROUP BY COURSE_CODE, YEAR
```