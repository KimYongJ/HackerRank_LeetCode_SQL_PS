- weather-observation-station-17
  - [https://www.hackerrank.com/challenges/weather-observation-station-17/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-17/problem?isFullScreen=true)
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
  ('City1', 'State1', 37.7749, -122.4194),
  ('City2', 'State2', 34.0522, -118.2437),
  ('City3', 'State3', 40.7128, -74.0060);
  ```
  - **문제 :** STATION 테이블에서 LAT_N 컬럼이 38.7780 보다 큰 값들 중 가장 작은 LAT_N 컬럼 값에 해당하는 LONG_W 값을 출력하는 문제 입니다. 단, LONG_W 컬럼 출력시 소수점 5자리에서 반올림하여 4자리까지 출력해주세요
  ```jsx
  [ 정답(1) ]
  SELECT ROUND(LONG_W,4)
  FROM STATION
  WHERE LAT_N = (
  				SELECT MIN(LAT_N)
  				FROM STATION
  				WHERE LAT_N > 38.7780
  			  )
  [ 정답(2) ]
  SELECT LW
  FROM (
  		SELECT 	ROUND(LONG_W,4) LW
  		,		RANK() OVER(ORDER BY LAT_N) RNK
  		FROM STATION
  		WHERE LAT_N > 38.7780
  	)ST
  WHERE RNK = 1
  ```
