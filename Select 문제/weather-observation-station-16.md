- weather-observation-station-16
  - [https://www.hackerrank.com/challenges/weather-observation-station-16/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-16/problem?isFullScreen=true)
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
  - **문제 :** STATION 테이블에서 LAT_N 컬럼 값이 38.7780 보다 큰 것들 중 가장 최소값인 LAT_N값을 출력하는 문제입니다. 출력시 소수점 4자리까지 표현하는데 그 이하는 반올림 하는 문제입니다. 간단한 예제라 해설은 생략합니다.
  ```jsx
  [ 정답 ]
  SELECT ROUND(MIN(LAT_N),4)
  FROM STATION
  WHERE LAT_N > 38.7780
  ```
