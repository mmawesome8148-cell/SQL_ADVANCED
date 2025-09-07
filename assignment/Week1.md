# SQL_ADVANCED 1주차 정규 과제
<span style="font-size:20px;"> **📌Week 1 : 서브쿼리 & CTE** 

<span style="font-size:18px;">1️⃣ **학습 내용**      
    <br>
2️⃣ **학습 내용 정리하기**
1. 서브쿼리 
 
   ✅ 학습 목표 : SubQueries에 대한 문법을 이해하고 활용할 수 있다.  

   <br>
    (0) 서브쿼리란?
    
    - 서브쿼리는 하나의 `SELECT`문(외부 쿼리) 안의 또다른 `SELECT`문  
    - 반드시 괄호로 감싸져야 함  
    - 복잡한 `JOIN`, `UNION`을 대체할 수 있음  
    - 서브쿼리를 이용하면 구조를 더 읽기 쉬움  
    - 서브쿼리 결과 형태:  
         **Scalar** (단일 값)  
         **Column** (단일 컬럼, 여러 행 가능)  
           **Row** (단일 행, 여러 컬럼 가능)  
           **Table** (다수 행, 다수 컬럼)  
   
   <br> 
    (1) 스칼라 서브쿼리: 단일 값 반환  
    
    - 하나의 셀값 `'abcde'`를 반환하고, `NULL` 값도 가능함.  - 그러나 리터럴 값만 허용하는 일부 문법에서는 사용할 수 없음.  
    - `expression`의 일부로도 사용 가능  
<br>

    (2) 비교연산자를 활용한 서브쿼리  
    - `JOIN` 으로는 불가능한 비교나 집계를 하는 경우
    - 예) 특정 값이 2번 등장하는 경우 찾기

    <br>
    (3) ANY, IN, SOME을 활용한 서브쿼리  

     - `JOIN`으로는 불가능한 비교나 집계를 하는 경우  
     - 예) 특정 값이 2번 등장하는 경우 찾기
     - `ANY`: 비교연산자 '뒤'에 위치, 하나라도 조건을 만족하면 `TRUE` 
     - `IN`: `ANY`의 별칭, 그러나 `ANY`와 달리 표현식도 받을 수 있음.
     - `SOME`: `ANY`의 또다른 별칭, 더 명확한 의미전달 가능
    
    <br>
    (4) ALL을 이용한 서브쿼리
    
     - 비교연산자 뒤에 위치
     - 모든 비교 결과가 TRUE일 때 `TRUE` 
     - 빈 테이블이면 결과는 조건에 따라 `TRUE` 아니면 `NULL`
     - `NOT IN`=`ALL`의 별칭
     - TABLE 구문 지원됨
     <br> (단, 단일컬럼인 경우/ 컬럼 표현식에 의존하지 않는 경우)

     <br>
    (4) 로우 서브쿼리: 하나의 행을 반환, (여러 개의 컬럼 ok)

     - Row Constructor와 Row 서브쿼리가 반환하는 행은 동일 개수의 값을 가져야
     - 단일 컬럼만 반환하면 문법 오류 발생

     <br>
    (5) EXISTS, NOT EXISTS를 활용한 서브쿼리
    
     - `EXISTS`: 한 행이라도 반환되면 TRUE
     - `NOT EXISTS`: 아무 행도 반환되지 않으면 TRUE
     - TABLE 구문 지원됨

      <br>
    (6) 상관 서브쿼리: 서브쿼리에서 외부쿼리에 있는 테이블을 참조할 때

    - 스코프 규칙: 안쪽 > 바깥쪽 순으로 평가됨.
    - 옵티마이저 최적화: 파생 테이블+`JOIN`으로 변환 가능
    <br> * 변환 가능 조건 - SELECT, WHERE(AND만), HAVING절/ =연산자
    <br> **변환 '불가능' 조건 - JOINM LIMIT, OFFSET, UNION, <=>연산자, 집계 함수 내부, 모든 절(WHERE제외)에는 상관 컬럼 불가 

***
<br>   
2. CTE

✅ 학습 목표 : CTE에 대한 문법을 이해하고 활용할 수 있다. 

(0) CTE란?

- 'Common Table Expressions'으로 하나의 SQL문 내에서만 존재하는 임시 결과 집합  
- `WITH`절은 `SELECT`, `UPDATE`, `DELETE`문 앞에 위치  
- 하나의 문장에는 `WITH`절 하나만  
- 해석 순서: 서브쿼리 > CTE > 기본 테이블  
- 이름: 지정하지 않으면 첫번째 SELECT문의 컬럼명으로 지정됨  

<br>

(1) CTE vs. Derived Tables

- 공통점: 이름 있음, 단일 문장에서만 존재  
- 차이점: CTE는 여러 번 참조, 자기 참조 가능, 가독성 좋음

***
<br>

<span style="font-size:18px;">3️⃣ **실습 문제**
<br>
- **프로그래머스 문제**
https://school.programmers.co.kr/learn/courses/30/lessons/131123

    즐겨찾기가 가장 많은 식당 정보 출력하기 (GROUP BY, SubQuery) : Lev 3

    https://school.programmers.co.kr/learn/courses/30/lessons/131115

    가격이 제일 비싼 식품의 정보 출력하기 (SUM, MAX, MIN, SubQuery) : Lev 2
<br><br>

- ️**문제 인증란**

    [즐겨찾기가 가장 많은 식당 정보 출력하기_SubQuery](./images/1.jpg)
    
    [즐겨찾기가 가장 많은 식당 정보 출력하기_채점결과](./images/2.jpg)
    <br><br>

    [가격이 제일 비싼 식품의 정보 출력하기_SubQuery](./images/3.jpg)

    [가격이 제일 비싼 식품의 정보 출력하기_CTE](./images/4.jpg)

    [가격이 제일 비싼 식품의 정보 출력하기_채점결과](./images/5.jpg)
<br><br>

- **문제 1**🧚
<br>예린이는 최근 여러 주문 데이터를 분석하는 업무를 맡게 되었습니다. 특정 고객의 주문 이력을 분석하기 위해, 다음과 같이 최근 30일간 주문만 필터링한 CTE를 사용해 쿼리를 작성했습니다.

```sql
WITH RecentOrders AS (
  SELECT *
  FROM Orders
  WHERE order_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY)
)
SELECT customer_id, COUNT(*) AS recent_order_count
FROM RecentOrders
GROUP BY customer_id;

그런데 예린이는 "이 쿼리를 WITH 없이, 서브쿼리 방식으로 바꿔서 실행해보라" 는 피드백을 받았고, 서브쿼리로 작성해보려 했지만 익숙하지 않아 SQL_ADVANCED를 듣는 학회원분들에게 도움을 요청하고 있습니다. 예린이의 쿼리를 WITH 없이 서브쿼리로 변환해보세요. 그리고 두 방식의 차이점을 설명해보고, 각각의 장단점을 정리해보세요


<서브쿼리를 활용한 방식>
SELECT customer_id
     , COUNT(*) AS recent_order_count
FROM (
  SELECT *
  FROM Orders
  WHERE order_date >= DATE_SUB(CURDATE(), INTERVAL 30 DAY)
) AS RecentOrders
GROUP BY customer_id;

<CTE vs. SubQuery>
- 차이점 (1) CTE는 여러번 참조할 수 있음.
        (2) 쿼리의 위치가 상이함.

- CTE 장점: 여러번 사용할 수 있고, 가독성이 좋음.
      단점: 그러나 CTE가 여러번 중첩되면 오히려 가독성이 떨어짐.

- SubQuery 장점: 간단한 쿼리에서는 구조 파악이 쉬움
           단점: 재사용 불가하고, 쿼리가 복잡해질수록 가독성 저하됨.

🎉 수고하셨습니다.