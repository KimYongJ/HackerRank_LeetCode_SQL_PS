- weather-observation-station-2
  - [https://www.hackerrank.com/challenges/weather-observation-station-2/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-2/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE STATION (
      ID INT PRIMARY KEY,
      CITY VARCHAR(100),
      STATE VARCHAR(100),
      LAT_N FLOAT,
      LONG_W FLOAT
  );
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES
  (1, 'City1', 'State1', 37.768, -122.424),
  (2, 'City2', 'State2', 36.778, -119.417),
  (3, 'City3', 'State3', 34.052, -118.243);
  ```
  - **문제 :** STATION 테이블의 LAT_N 값의 합계와 LONG_W 값의 합계를 구합니다. 단 소숫점 2자리수에서 반올림 합니다.
  ```jsx
  [ 정답 ]
  SELECT     ROUND(SUM(LAT_N),2)
  ,         ROUND(SUM(LONG_W),2)
  FROM STATION
  ```
  - **해설 :** SUM함수로 합계를 구한 후, ROUND함수로 반올림을 합니다.
    - **ROUND 함수 :** 해당 함수는 첫 번째인자로 반올림할 숫자를 전달하고, 두 번째 인자는 소수점 이하 몇 번째 자리까지 반올림할지를 지정하는 정수를 전달합니다. 1을 전달하면 출력으로 소수점 1자리까지 출력이됩니다.(이하는 반올림 처리) 2를 전달하면 소수점 2자리까지 출력됩니다.(이하는 반올림 처리)
