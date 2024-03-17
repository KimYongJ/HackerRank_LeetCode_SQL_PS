# **Last-Person-to-Fit-in-the-Bus**

- [https://leetcode.com/problems/last-person-to-fit-in-the-bus/](https://leetcode.com/problems/last-person-to-fit-in-the-bus/)
- **문제 :** 버스에 탈 수 있는 사람들의 명단을 관리하는 상황입니다. 버스의 최대 하중은 1000kg이며, trun 컬럼을 기준으로 순서 대로 버스에 탈 때 버스 최대 하중을 초과하지 않고 타는 가장 마지막 사람의 이름을 출력하는 문제입니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Queue (
    person_id int,
    person_name varchar(255),
    weight int,
    turn int
);
INSERT INTO Queue (person_id, person_name, weight, turn) VALUES
(1, 'Alice', 250, 1),
(4, 'Bob', 175, 5),
(3, 'Alex', 350, 2),
(6, 'John Cena', 400, 3),
(2, 'Marie', 200, 4),
(1, 'Winston', 500, 6);
```

```jsx
[ 정답 ]
SELECT PERSON_NAME
FROM(
	SELECT	SUM(WEIGHT) OVER(ORDER BY TURN) TOTAL
	,		PERSON_NAME
	FROM QUEUE
)TEMP
WHERE TOTAL <= 1000
ORDER BY TOTAL DESC
LIMIT 1
```

- **해설 :** 윈도우 함수를 사용해 TURN 컬럼을 기준으로 점진적인 합계를 구해나갑니다. 아래는 이렇게 구한 서브 쿼리 실행 결과 입니다.
  사진(1)
  그 후 TOTAL 컬럼이 1000을 넘지 않는 행들을 TOTAL값 기준으로 내림차순 정렬합니다. 하나만 출력 해야하기 때문에 마지막에 LIMIT 1로 한 줄만 출력 되도록 합니다.
