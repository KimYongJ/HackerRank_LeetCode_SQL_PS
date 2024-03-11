- **Rising-Temperature**

  - [https://leetcode.com/problems/rising-temperature/](https://leetcode.com/problems/rising-temperature/)
  - **문제 :** Weather 테이블에서 RECORDDATE 컬럼을 기준으로 하루 전날의 온도보다 오늘 온도가 더 클 때의 ID를 출력합니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Weather (
      id INT PRIMARY KEY,
      recordDate DATE,
      temperature INT
  );

  INSERT INTO Weather (id, recordDate, temperature) VALUES
  (1, '2015-01-01', 10),
  (2, '2015-01-02', 25),
  (3, '2015-01-03', 20),
  (4, '2015-01-04', 30);
  ```

  ```jsx
  [ 정답 ]
  	SELECT 	W1.ID
  	FROM WEATHER W1
  	INNER JOIN WEATHER W2
  	ON W2.RECORDDATE = DATE_SUB(W1.RECORDDATE, INTERVAL 1 DAY)
  	WHERE W1.TEMPERATURE > W2.TEMPERATURE
  ```

  - **해설 :** 하루 전날을 구하기 위해 DATE_SUB 함수를사용 합니다. 이 함수는 날짜를 첫번째 인자로 받고, 두번 째 인자로 뺄 값을 넣습니다. 하루를 빼줘야 하기 때문에 1 DAY를 적었으며 초, 분, 시간, 달 등을 빼고 싶다면 각각 **INTERVAL** 1 **SECOND** , **INTERVAL** 1 **MINUTE** , **INTERVAL** 1 **HOUR** , **INTERVAL** 1 **MONTH**을 적어 줍니다. 간단하게 하기 위해 조인 조건을 날짜로 잡고 WHERE 조건에서 온도를 비교해 주었습니다.
