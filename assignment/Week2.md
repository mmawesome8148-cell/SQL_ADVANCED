# SQL_ADVANCED 2주차 정규 과제
### Week 2 :집합 연산자 & 그룹 함수
📌SQL_ADVANCED 정규과제는 매주 정해진 주제에 따라 MySQL 공식 문서 또는 한글 블로그 자료를 참고해 개념을 정리한 후, 프로그래머스/ Solvesql / LeetCode에서 SQL 3문제와 추가 확인문제를 직접 풀어보며 학습하는 과제입니다.

이번 주는 아래의 SQL_ADVANCED_2nd_TIL에 나열된 주제를 중심으로 개념을 학습하고, 주차별 학습 목표에 맞게 정리해주세요. 정리한 내용은 GitHub에 업로드한 후, 스프레드시트의 'SQL' 시트에 링크를 제출해주세요.

👀 (수행 인증샷은 필수입니다.)

프로그래머스 문제를 풀고 '정답입니다' 문구를 캡쳐해서 올려주시면 됩니다.

## SQL_ADVANCED_2nd
### 1. 집합 연산자

15.2.18. UNION Clause
15.2.14. Set Operations with UNION, INTERSECT
UNION, UNION ALL 중심으로 개념을 정리하고, INTERSECT, EXCEPT는 구문이 어떤 기능을 하는지 간단히만 알아봅니다. EXCEPT와 INTERSECT는 대부분 MySQL 버전에서 공식 지원되지 않기 때문에, 이번주 학습은 UNION, UNION ALL 만 집중적으로 정리해주세요.

### 2. 그룹 함수 (집계 함수)

14.19.1. Aggregate Function Descriptions <br>
🏁 주차별 학습 (Study Schedule) <br>
주차	공부 범위	완료 여부 <br>
1주차	서브쿼리 & CTE	✅ <br>
2주차	집합 연산자 & 그룹 함수	✅ <br>
3주차	윈도우 함수	🍽️ <br>
4주차	Top N 쿼리	🍽️ <br>
5주차	계층형 질의와 셀프 조인	🍽️ <br>
6주차	PIVOT / UNPIVOT	🍽️ <br>
7주차	정규 표현식	🍽️ <br>

공식 문서 활용 팁
MySQL 공식 문서는 영어로 제공되지만, 크롬 브라우저에서 공식 문서를 열고 이 페이지 번역하기에서 한국어를 선택하면 번역된 버전으로 확인할 수 있습니다. 다만, 번역본은 문맥이 어색한 부분이 종종 있으니 영어 원문과 한국어 번역본을 왔다 갔다 하며 확인하거나, 교육팀장의 정리 예시를 참고하셔도 괜찮습니다.

## 1️⃣ 학습 내용
아래의 링크를 통해 MySQL 공식문서로 이동하실 수 있습니다.

15.2.18. UNION Clause : MySQL 공식문서
https://dev.mysql.com/doc/refman/8.0/en/union.html

15.2.14. Set Operations with UNION, INTERSECT : MySQL 공식문서
https://dev.mysql.com/doc/refman/8.0/en/set-operations.html

(한국어 버전) https://dart-b-official.github.io/posts/mysql-UNION/

14.19.1. Aggregate Function Descriptions : MySQL 공식문서
https://dev.mysql.com/doc/refman/8.0/en/aggregate-functions.html

(한국어 버전) https://dart-b-official.github.io/posts/mysql-aggregate_function/ 

## 2️⃣ 학습 내용 정리하기
### 1. 집합 연산자
#### ✅ 학습 목표 :
* UNION과 UNION ALL의 차이와 사용법을 이해한다.
* 중복 제거 여부, 컬럼 정렬 조건 등을 고려하여 올바르게 집합 연산자를 사용할 수 있다. 

#### ✅ 내용 정리 :
- `UNION`: 여러 테이블을 연결하여 하나의 테이블로 합치는 집합 연산자 + 중복되는 행은 제거하고 한 개만 남김. 
 <pre> mysql> SELECT 1, 2;
+---+---+
| 1 | 2 |
+---+---+
| 1 | 2 |
+---+---+
mysql> SELECT 'a', 'b';
+---+---+
| a | b |
+---+---+
| a | b |
+---+---+
mysql> SELECT 1, 2 UNION SELECT 'a', 'b';
+---+---+
| 1 | 2 |
+---+---+
| 1 | 2 |
| a | b |
+---+---+ </pre>

    !주의! 
    1) UNION으로 묶이는 테이블의 컬럼 수, 데이터 타입이 일치해야 
    2) `UNION`과 함께 쓰려면 잠금절을 반드시 괄호로 묶어야 함. 

- `INTERSECT`: 두 쿼리 블록에 공통으로 존재하는 행만 반환 (교집합)
- `EXCEPT`: 두 쿼리 블록 A, B에서 A에만 존재하고 B에는 없는 행 반환

- `ALL`: 중복되는 행을 제거하지 않음.
- `DISTINCT`: 중복 제거 (기본 동작) <br>
*`ALL`과 혼합 사용시 `DISTINCT`가 우선 적용됨. 

- **연산자 우선 순위**: `INTERSECT` > `UNION`, `EXCEPT`
- **교환법칙**: 순서가 바뀌어도 결과는 똑같음. (`UNION`, `INTERSECT`) => `EXCEPT`는 성립하지 않음. 

- **TABLES/ VALUES문과 집합 연산**
    - `TABLES`: 전체 데이터 불러오기
    - `VALUES`: 작은 임시 테이블 만들기

- **ORDER BY와 LIMIT**
    - 별칭을 쓴 경우 `ORDER BY`에서 반드시 별칭 사용
    - `ORDER BY`절에서 집계 함수 사용 불가 
***


### 2. 그룹함수
✅ 학습 목표 :
* COUNT, SUM, AVG, MAX, MIN 함수의 기본 사용법을 익힌다.
* GROUP BY와 HAVING 절을 적절히 활용할 수 있다.
* NULL과 집계 함수가 어떻게 상호작용하는지 이해한다. 

#### ✅ 내용 정리 :

- `COUNT`: 행 수 반환
- `SUM`: 합계 반환
- `AVG`: 평균 반환
- `MAX`: 최댓값 반환
    - 문자열 인자 가능
- `MIN`: 최솟값 반환
- `GROUP BY`: 부분집합으로 나누어 집계하는 함수 -> 없으면 모든 행을 하나의 그룹으로 집계한다는 것
- `HAVING`: 그룹별로 집계한 후 특정 값을 추출하고 싶을 때 사용함. 

- `DISTINCT`는 서로 다른 값들끼리의 집계

- `BIT_AND`: 모든 비트에 대해 AND
- `BIT_OR`: 모든 비트에 대해 OR
- `BIT_XOR`: 모든 비트에 대한 XOR

- `GROUP CONCAT`: 여러 행의 문자열 값을 하나의 문자열로 합쳐주는 함수

- `NULL`: 집계할 때 NULL만 있는 경우, NULL 반환. 이외의 경우에는 대부분 무시되거나 DISTINCT 써서 제외시킴. 



## 3️⃣ 실습 문제
https://leetcode.com/problems/customers-who-never-order/

LeetCode 183. Customers Who never Order
<pre> SELECT c.name AS Customers
 FROM Customers AS c
      LEFT JOIN Orders AS o ON c.id = o.customerId
 WHERE o.id IS NULL;</pre>

학습 포인트 : 주문 내역이 없는 고객을 찾기 위한 패턴 익히기

https://leetcode.com/problems/department-highest-salary/description/

LeetCode 184. Department Highest Salary

학습 포인트 : 부서별 최고 연봉자 추출을 위한 그룹별 정렬 / 필터링 방식 이해하기

<pre>SELECT d.name AS Department
      , e.name AS Employee
      , e.salary AS Salary
FROM Employee AS e
     JOIN Department AS d ON e.departmentId = d.id
WHERE e.salary = (SELECT MAX(salary)
                  FROM Employee
                  WHERE departmentId = e.departmentId) </pre>


## 문제 인증란
### 확인문제
문제 1
🧚동혁이는 SQL 문제를 풀면서 UNION과 UNION ALL의 차이를 명확히 이해하지 못해 중복된 값이 생기거나 누락되는 문제를 계속 겪고 있습니다.

 아래는 동혁이가 작성한 쿼리입니다.
<pre> SELECT name 
 FROM member
      UNION SELECT name FROM blackList; </pre>

그런데 예상과 달리 blacklist에만 있는 이름이 결과에 안 나오거나, 중복된 이름이 사라져서 헷갈리고 있습니다.

 UNION과 UNION ALL의 차이를 설명하고, 중복 포함 여부에 따라 어떤 경우에 어떤 쿼리를 써야 하는지 예시와 함께 설명해주세요


UNION은 두 쿼리블록을 결합한 후 중복되는 행을 제거하고 한 개만 남기지만 UNION ALL은 중복되는 행을 모두 남겨둔다. 위의 예시처럼 중복 상관없이 블랙리스트에 있는 모든 이름을 보고싶으면 UNION ALL을 쓰고, 중복없이 보고싶으면 UNION을 쓰는 것이 적절하다. 

## 참고자료
그룹 함수가 많아서 중요하게 많이 쓰이는 함수들을 정리해놓은 참고자료를 첨부합니다. 아래 블로그를 통해서 더욱 쉽게 공부해보시고 문제를 풀어보세요.

[SQL 10] 그룹 함수, GROUP BY 절, HAVING 절 <br> https://keep-cool.tistory.com/37

또한, MySQL 문서 이외에 Oracle 함수에서 사용하는 그룹함수에 대한 소개도 같이 첨부합니다. SQLD 시험 준비하시는 분이 있다면 이 자격증 시험에서는 Oracle 언어를 기반으로 문제가 출제하오니 아래 블로그도 같이 공부해보세요. (선택사항입니다.) <br> 2. 그룹 함수 (Group FUNCTION) https://dkkim2318.tistory.com/48
<br>



🎉 수고하셨습니다.