# **Investments-in-2016**

- [https://leetcode.com/problems/investments-in-2016/](https://leetcode.com/problems/investments-in-2016/)
- **문제**
  - 아래 조건을 만족하는 행들의 2016년 투자 가치(`tiv_2016`)의 합계를 계산해야 합니다.
    - **2015년 투자 가치가 동일한 정책**: `tiv_2015` 값이 다른 행들과 같은 행들만 고려합니다. 예를 들어, `tiv_2015`가 10인 모든 행들이 이 조건에 해당됩니다.
    - **전체 행에서 위치가 유일한 정책**: 같은 위도(`lat`)와 경도(`lon`) 값을 갖지 않는 행들만 합계를 계산에 포함합니다. 즉, 같은 도시에 있는 여러 보험 정책은 고려하지 않습니다.
  - 이 두 조건을 모두 만족하는 행들에 대해서만 `tiv_2016` 값을 더하여 그 합계를 구해야 합니다. 그 결과는 소수점 둘째 자리까지 표시해야 합니다(예: 45.00)

```jsx
[ 문제 조건 ]
CREATE TABLE Insurance (
    pid INT PRIMARY KEY,
    tiv_2015 FLOAT,
    tiv_2016 FLOAT,
    lat FLOAT NOT NULL,
    lon FLOAT NOT NULL
);
INSERT INTO Insurance (pid, tiv_2015, tiv_2016, lat, lon) VALUES
(1, 10.0, 5.0, 10.0, 10.0),(2, 20.0, 20.0, 20.0, 20.0),
(3, 10.0, 30.0, 20.0, 20.0),(4, 10.0, 40.0, 40.0, 40.0);
```

```jsx
[ 정답(1) ]
SELECT	ROUND(SUM(TIV_2016), 2) TIV_2016
FROM INSURANCE
WHERE TIV_2015 IN(
					SELECT	TIV_2015
					FROM INSURANCE
					GROUP BY TIV_2015
					HAVING COUNT(*)>1
				)
AND (LAT, LON) IN(
					SELECT LAT, LON
					FROM INSURANCE
					GROUP BY LAT, LON
					HAVING COUNT(*) = 1
				)
[ 정답(2) ]
WITH TEMP1 AS(
			SELECT	TIV_2015
			FROM INSURANCE
			GROUP BY TIV_2015
			HAVING COUNT(*)>1
),
TEMP2 AS(
		SELECT LAT, LON
		FROM INSURANCE
		GROUP BY LAT, LON
		HAVING COUNT(*) = 1
)
SELECT	ROUND(SUM(TIV_2016), 2) TIV_2016
FROM INSURANCE I
WHERE EXISTS (
	SELECT 1 FROM TEMP1 T1 WHERE T1.TIV_2015 = I.TIV_2015
)
AND
EXISTS(
	SELECT 1 FROM TEMP2 T2 WHERE T2.LAT = I.LAT AND T2.LON = I.LON
)
```

- **정답(1) 해설**
  - 문제 요구사항 그대로 IN을 사용해 TIV_2015의 값이 2개 이상인 행들과, LAT, LON 값을 그룹지었을 때 하나인 행을 걸러내고 TIV_2016의 값을 SUM 함수를 통해 합쳐 줍니다. 출력할 때는 소수점 2자리까지 반올림해야 하므로 ROUND함수로 한번 감싸줍니다.
- **정답(2) 해설**
  - 정답(1)에서 IN 키워드를 사용했다면 정답(2)에서는 EXISTS를 사용합니다. 이를 위해 WITH절로 각 서브쿼리들을 분리해 넣어 놓고 EXISTS 키워드 안 WHERE 조건에서 조건에 맞는 행들만 걸러냅니다.
