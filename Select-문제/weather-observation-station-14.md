- weather-observation-station-14
  - [https://www.hackerrank.com/challenges/weather-observation-station-14/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-14/problem?isFullScreen=true)
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
  (1, 'City1', 'State1', 37.7749, -122.4194),
  (2, 'City2', 'State2', 34.0522, -118.2437),
  (3, 'City3', 'State3', 40.7128, -74.0060);
  ```
  - **문제 :** STATION 테이블에서 LAT_N 컬럼 값이 137.2345 보다 작은 것들 중 가장 큰 LAT_N 컬럼 값을 출력하는 문제입니다. 단, 소숫점 4자리 이하는 버려야 합니다.
  ```jsx
  [ 정답 ]
  SELECT TRUNCATE(MAX(LAT_N),4)
  FROM STATION
  WHERE LAT_N <137.2345
  ```
