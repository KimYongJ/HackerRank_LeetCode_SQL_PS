- weather-observation-station-13
  - [https://www.hackerrank.com/challenges/weather-observation-station-13/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-13/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE STATION (
      ID INT PRIMARY KEY,
      CITY VARCHAR(100),
      STATE VARCHAR(100),
      LAT_N DECIMAL(9, 6),
      LONG_W DECIMAL(9, 6)
  );
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES
  (1, 'City1', 'State1', 40.7128, -74.0060),
  (2, 'City2', 'State2', 34.0522, -118.2437),
  (3, 'City3', 'State3', 41.8781, -87.6298);
  ```
  - **문제 :** STATION 테이블에서 LAT_N 값이 38.7800 보다 크고, 137.2345 보다 작은 LAT_N값의 합계를 구하는데 소수점 4자리 이하는 버림하는 문제입니다.
  ```jsx
  [ 정답 ]
  SELECT TRUNCATE(SUM(LAT_N),4)
  FROM STATION
  WHERE LAT_N > 38.7800
  AND LAT_N < 137.2345
  ```
