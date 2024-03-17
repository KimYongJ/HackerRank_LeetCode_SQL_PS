# **Restaurant Growth 이동평균문제**

- [https://leetcode.com/problems/restaurant-growth/](https://leetcode.com/problems/restaurant-growth/)
- **문제 :** 고객이 지불한 금액의 이동 평균을 계산하고자 합니다. 이동 평균은 특정 날짜를 포함하여 그 날짜로부터 이전 6일 간의 평균을 의미합니다. 예를 들어, 2019년 1월 10일의 이동 평균은 1월 4일부터 1월 10일까지의 평균 금액을 말합니다. SQL 쿼리를 작성하여 각 날짜의 이동 평균을 계산하고, 결과를 'visited_on' 날짜 기준으로 오름차순으로 정렬해야 합니다. 결과는 소수점 아래 두 자리까지 반올림하여 표시해야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Customer (
    customer_id int,
    name varchar(255),
    visited_on date,
    amount int
);
INSERT INTO Customer (customer_id, name, visited_on, amount) VALUES
(1, 'Jhon', '2019-01-01', 100),
(2, 'Daniel', '2019-01-02', 110),
(3, 'Jade', '2019-01-03', 120),
(4, 'Khaled', '2019-01-04', 130),
(5, 'Winston', '2019-01-05', 110),
(6, 'Elvis', '2019-01-06', 140),
(7, 'Anna', '2019-01-07', 150),
(8, 'Maria', '2019-01-08', 80),
(9, 'Jaze', '2019-01-09', 110),
(1, 'Jhon', '2019-01-10', 130);
```

```jsx
[ 정답 ]
SELECT 	VISITED_ON
,		AMOUNT
,		AVERAGE_AMOUNT
FROM(
		SELECT 	SUM(C0.AMOUNT) OVER(ORDER BY C0.VISITED_ON ROWS BETWEEN 6 PRECEDING AND CURRENT ROW) AMOUNT
		,		ROUND(AVG(C0.AMOUNT) OVER(ORDER BY C0.VISITED_ON ROWS BETWEEN 6 PRECEDING AND CURRENT ROW),2) AVERAGE_AMOUNT
		,		C0.VISITED_ON
		FROM(
				SELECT 	SUM(AMOUNT) AMOUNT
				,		VISITED_ON
				FROM CUSTOMER
				GROUP BY VISITED_ON
		)C0
)C1
WHERE EXISTS(
	SELECT 1
	FROM CUSTOMER C2
	WHERE C2.VISITED_ON = DATE_SUB(C1.VISITED_ON,INTERVAL 6 DAY)
)
ORDER BY VISITED_ON
```

- **해설**
  - 먼저 테이블명 ‘C0’ 쪽 쿼리를 보면, 서브 쿼리에서 VISITED_ON 컬럼 기준으로 그룹핑하여 SUM(AMOUNT)를 구해주고 있습니다. 이렇게 하는 이유는 같은 날에 결제한 고객이 여러명일 경우 한 줄로 만들어 주기 위해서 입니다.
  - 그렇게 GROUPING 한 VISITED_ON 컬럼과 AMOUNT 컬럼을 갖고 오늘과 6일 전까지의 급액의 합계(SUM)와 평균(AVG)을 구합니다. 이 때 평균은 소수점 2째 자리까지 표현 해야 하기 때문에 ROUND함수로 감싸줍니다.
  - 6일 전까지 행을 구하기 위해 윈도우 함수를 사용합니다. ( **ORDER** **BY** C0.VISITED_ON **ROWS** **BETWEEN** 6 **PRECEDING** **AND** **CURRENT** **ROW )**
  - 위에서 사용한 윈도우 함수를 설명하면 아래와 같습니다.
    - **ORDER BY C0.VISITED_ON :** 행을 VISITED_ON 컬럼 기준으로 오름차순 정렬합니다.
    - **ROWS** : 뒤에 나오는 범위로 데이터 구간을 한정한다는 의미입니다.
    - **BETWEEN** **6 PRECEDING** **AND** **CURRENT** **ROW :** 현재 행(CURRENT ROW) 과 6행 전까지(6 PRECEDING) 사이(BETWEEN)를 구간으로 한다는 의미입니다.
  - 테이블명 C0의 실행 결과는 아래와 같습니다.
  
  ![사진1](https://github.com/KimYongJ/HackerRank_LeetCode_SQL_PS/assets/106525587/9426ab50-db3b-4626-a035-8d2dbb95887e)

  - 위 사진에서 보듯이 이전 일주일치 결제 금액 합계와, 평균이 잘 구해졌습니다. 여기서 추가적으로 일주일을 다 채우지 못하는, 그러니까 현 행의 VISITED_ON 날짜 보다 6일 전 행이 없는 컬럼들은 걸러주어야 합니다. 이를 위해 EXISTS 키워드를 사용합니다. 오늘 날짜 기준으로 6일전 행이 있는 데이터만 화면에 출력해줍니다.
  
   ![사진2](https://github.com/KimYongJ/HackerRank_LeetCode_SQL_PS/assets/106525587/60ea868f-2b9e-49a3-8bba-6248718de941)
