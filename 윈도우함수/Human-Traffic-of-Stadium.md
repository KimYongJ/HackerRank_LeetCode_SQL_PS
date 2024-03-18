# **Human-Traffic-of-Stadium**

- [https://leetcode.com/problems/human-traffic-of-stadium/](https://leetcode.com/problems/human-traffic-of-stadium/)
- **문제**
  - 연속된 id를 가진 세 개 이상의 행과 각각의 행에서 사람의 수가 100명 이상인 기록을 표시하는 솔루션을 작성하는 문제입니다.
  - 결과 테이블을 방문 날짜에 따라 오름차순으로 정렬합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Stadium (
    id INT,
    visit_date DATE,
    people INT
);

[ VERSION 1 ]
INSERT INTO Stadium (id, visit_date, people) VALUES
(1, '2017-01-01', 10),
(2, '2017-01-02', 109),
(3, '2017-01-03', 150),
(4, '2017-01-04', 99),
(5, '2017-01-05', 145),
(6, '2017-01-06', 1455),
(7, '2017-01-07', 199),
(8, '2017-01-09', 188);

[ VERSION 2 ]
INSERT INTO Stadium (id, visit_date, people) VALUES
(1, "2017-01-01", 10),
(2, "2017-01-02", 109),
(3, "2017-01-03", 150),
(4, "2017-01-04", 100);
```

```jsx
[ 정답 ]
SELECT	ID, VISIT_DATE, PEOPLE
FROM(
	SELECT	LAG(PEOPLE,1) OVER(ORDER BY ID) BEFORE1
	,		LAG(PEOPLE,2) OVER(ORDER BY ID) BEFORE2
	,		LEAD(PEOPLE,1) OVER(ORDER BY ID) AFTER1
	,		LEAD(PEOPLE,2) OVER(ORDER BY ID) AFTER2
	,		PEOPLE
	,		VISIT_DATE
	,		ID
	FROM STADIUM
)TEPM
WHERE PEOPLE >= 100
AND
(
	(BEFORE1 >= 100 AND BEFORE2 >= 100)
	OR
	(AFTER1 >= 100 AND AFTER2 >= 100)
	OR
	(BEFORE1 >=100 AND AFTER1 >= 100)
)
```

- **해설**
  - 사람 수가 100이 넘으면서 3번 연속된 아이디를 찾기 위해 LAG와 LEAD함수로 문제를 해결했습니다. 현재 행보다 위나 아래 데이터를 가져오려면 윈도우 함수 LAG와 LEAD를 사용할 수 있습니다.
- **LAG 함수**
  - 현재 행으로부터 지정된 수만큼 이전에 위치한 행의 데이터를 가져옵니다.
  - **형태**
    - LAG(value_expression, offset, default) OVER (
      [PARTITION BY partition_expression]
      ORDER BY sort_expression
      )
      - `value_expression`: 현재 행에서 가져올 열의 값입니다.
      - `offset`: 현재 행으로부터 얼마나 떨어진 행을 참조할 것인지 지정합니다. 기본값은 1입니다.
      - `default`: `offset`에 지정된 행이 존재하지 않을 경우 반환할 기본값입니다. 기본값은 `NULL`입니다.
      - `PARTITION BY`: 결과 집합을 특정 기준에 따라 분할하는 데 사용됩니다. 이를 통해 각 그룹 내에서 독립적으로 `LAG` 함수를 적용할 수 있습니다.
      - `ORDER BY`: `LAG` 함수가 참조할 행의 순서를 결정합니다.
        
- **LEAD 함수**
  - `LAG`의 반대로, 현재 행보다 이후에 위치한 행에서 데이터를 가져올 때 사용합니다. 예를 들어, 현재 행보다 한 행 후의 데이터를 가져오고 싶다면 `LEAD(column_name, 1)`을 사용합니다. `LEAD` 또한 옵셋을 이용하여 참조할 행의 거리를 지정할 수 있습니다.
