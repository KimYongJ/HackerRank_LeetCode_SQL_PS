# **Game-Play-Analysis-IV**

- [https://leetcode.com/problems/game-play-analysis-iv/](https://leetcode.com/problems/game-play-analysis-iv/)
- **문제 :** 플레이어들이 게임에 로그인하고 몇 게임을 했는지를 기록하는 테이블 `Activity`가 있습니다. 첫 로그인한 날부터 연속해서 두 날 동안 로그인한 플레이어의 비율을 구해야 합니다. 이 비율을 계산할 때는 소수점 두 번째 자리까지 반올림하여 나타내야 하며, 이는 전체 플레이어 수로 연속 로그인한 플레이어 수를 나누어 계산합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Activity (
  player_id INT,
  device_id INT,
  event_date DATE,
  games_played INT
);
INSERT INTO Activity (player_id, device_id, event_date, games_played) VALUES
(1, 2, '2016-03-01', 5),
(1, 2, '2016-03-02', 6),
(1, 2, '2016-03-03', 7),
(2, 2, '2017-06-25', 1),
(3, 1, '2016-03-02', 0),
(3, 4, '2018-07-03', 5);
```

```jsx
[ 정답 ]
SELECT	 ROUND( SUM(ISTRUE) / COUNT(DISTINCT PLAYER_ID), 2 ) FRACTION
FROM(
	SELECT	PLAYER_ID
	,		DATEDIFF(EVENT_DATE, MIN(EVENT_DATE) OVER(PARTITION BY PLAYER_ID)) = 1 AS ISTRUE
	FROM Activity
)TEMP
```

- **해설**
- **서브쿼리 ( TEMP 테이블 내용 ) 설명**
  - 먼저 기본 Activity 테이블에서 첫번 째 로그인하고 다음날까지 연속으로 로그인한 사람을 찾아야 합니다. 이를 위해 컬럼 ISTRUE 를 만들었습니다.
  - ISTRUE 설명
    - datediff 함수를 사용해 날짜 두개의 차이를 구합니다. 이때, MIN과 OVER 윈도우 함수를 사용해 첫째날을 구합니다. 그 후 DATEDIFF 함수의 실행 결과가 1과 같은지 체크합니다(코드: = 1 ) datediff 함수를 사용한 결과가 1인 경우에만 true가 반환되어 1로 표현됩니다. SQL에서 TRUE는 1로, FALSE는 0으로 표현됩니다.
- 그리고 TEMP 테이블 밖에서 집계함수 SUM과 COUNT를 사용해 연속으로 로그인한 사람의 비율을 구합니다. 이 때 GROUP BY절은 명시하지 않았는데 이렇게 할 경우 기본적으로 모든 행에 대해 전체 집계를 수행합니다. 그래야 결과가 단일행으로 반환됩니다.
