- weather-observation-station-15
  - [https://www.hackerrank.com/challenges/weather-observation-station-15/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-15/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE STATION (
      ID INT AUTO_INCREMENT PRIMARY KEY,
      CITY VARCHAR(100),
      STATE VARCHAR(100),
      LAT_N DECIMAL(10, 6),
      LONG_W DECIMAL(10, 6)
  );
  INSERT INTO STATION (CITY, STATE, LAT_N, LONG_W) VALUES
  ('City1', 'State1', 38.123456, -77.123456),
  ('City2', 'State2', 39.123456, -78.123456),
  ('City3', 'State3', 40.123456, -79.123456);
  ```
  - **문제 :** STATION 테이블에서 LAT_N 컬럼 값이 137.2345보다 작은 값 중 가장 큰 LAT_N의 컬럼을 뽑아 그 행에서 LONG_W 값을 출력하는 문제입니다. 이 때 LONG_W 는 소수점 4자리까지 표현하는데 반올림해서 표현합니다. 두가지 정답을 보여줍니다. 하나는 IN을 활용하고 하나는 RANK() 함수를 활용합니다. 간단한 예제라 해설은 생략했습니다.
  ```jsx
  [ 정답(1) ]
  SELECT ROUND(LONG_W,4)
  FROM STATION
  WHERE LAT_N IN (
  									SELECT MAX(LAT_N)
  									FROM STATION
  									WHERE LAT_N < 137.2345
  								)
  [ 정답(2) ]
  SELECT RW
  FROM (
  		SELECT 	ROUND(LONG_W,4) RW
  		,		RANK() OVER(ORDER BY LAT_N DESC) RNK
  		FROM STATION
  		WHERE LAT_N < 137.2345
  	)ST
  WHERE RNK = 1
  ```
