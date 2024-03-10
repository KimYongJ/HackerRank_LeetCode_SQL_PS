# **Queries-Quality-and-Percentage**

- [https://leetcode.com/problems/queries-quality-and-percentage/](https://leetcode.com/problems/queries-quality-and-percentage/)
- 문제 : 데이터베이스에서 수행된 몇몇 쿼리의 평가를 바탕으로 쿼리의 질을 평가하는 것입니다. 각 쿼리는 위치 값(1에서 500까지)과 평가 점수(1에서 5까지)를 가지며, 평가 점수가 3 미만인 쿼리를 '나쁜 쿼리' 라고 합니다. 출력은 모든 쿼리에 대해 평균 쿼리 질과 나쁜 쿼리의 비율을 구하는 것이며, 이 두 값은 소수점 둘째 자리까지 반올림해서 표현합니다. 평균 쿼리 질은 쿼리 평가(RATING )와 그 위치의 비율(POSITION) 평균이고, 나쁜 쿼리 비율은 전체 쿼리 중 평가가 3 미만인 쿼리의 쿼리 평가(RATING )의 평균의 백분율로 계산합니다. 이 때 출력은 QUERY_NAME이 값이 있을 때만 출력합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Queries (
  query_name VARCHAR(255),
  result VARCHAR(255),
  position INT,
  rating INT
);
INSERT INTO Queries (query_name, result, position, rating) VALUES
('Dog', 'Golden Retriever', 1, 5),
('Dog', 'German Shepherd', 2, 5),
('Dog', 'Mule', 200, 1),
('Cat', 'Shirazi', 5, 2),
('Cat', 'Siamese', 3, 3),
('Cat', 'Sphynx', 7, 4);
```

```jsx
[ 정답 ]
SELECT	QUERY_NAME
,		ROUND(AVG(RATING / POSITION), 2) AS QUALITY
,		ROUND(AVG(RATING < 3) * 100, 2) AS POOR_QUERY_PERCENTAGE
FROM QUERIES
WHERE QUERY_NAME IS NOT NULL
GROUP BY QUERY_NAME
```
