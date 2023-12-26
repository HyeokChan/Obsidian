# 인덱스
### 인덱스의 필요성
- 데이터베이스에 저장된 자료를 더욱 빠르게 조회하기 위해 인덱스를 생성하여 사용함
- 일반적으로 10~15% 이하의 데이터를 처리하는 경우에 효율적, 그 이상의 데이터를 처리할 땐 인덱스를 사용하지 않는 것이 더 나음
### B\*TREE 구조
- 인덱스의 데이터 저장 방식
- ROOT, BRANCH, LEAF NODE로 구성
![[Pasted image 20231226153522.png]]
- B\*TREE 구조의 핵심은 SORT
1. 인덱스를 사용하면 ORDER BY에 의한 SORT를 피할 수 있음
2. MAX/MIN의 효율적인 처리가 가능함

### 인덱스 활용 예시
- (COURSE_CODE, YEAR, COURSE_SQ_NO)로 구성된 인덱스 EC_COURSE_SQ_PK가 있음
```
SELECT COURSE_CODE, YEAR, COURSE_SQ_NO
FROM EC_COURSE_SQ
WHERE COURSE_CODE = 1960
AND YEAR = '2022'
ORDER BY COURSE_SQ_NO DESC
```
```
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
![[Pasted image 20231226154906.jpg]]
- MIN, MAX를 동시에 구하여 인덱스를 사용할 수 있음에도 실행계획에 SORTING이 발생함
![[Pasted image 20231226155131.jpg]]
```
A.COURSE_SQ_NO AS MAX_SQ FROM EC_COURSE_SQ A WHERE A.COURSE_CODE = 1960 AND A.YEAR = '2002' AND ROWNUM = 1
```
- MIN, MAX를 분리해서 구하고 UNION ALL을 사용하여 각각의 값을 구할 때 인덱스를 활용할 수 있도록 개선

---


