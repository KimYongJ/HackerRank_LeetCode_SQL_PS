- weather-observation-station-18
  - [https://www.hackerrank.com/challenges/weather-observation-station-18/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-18/problem?isFullScreen=true)
  - **문제 :** 평면 상의 두점 P1(a, b) 와 P2(c,d) 사이의 맨해튼 거리를 구하는 문제입니다. a와 c는 각각 LAT_N 컬럼의 최소 값과 최대값입니다. b와 d는 각각 LONG_W 컬럼의 최소값과 최대값입니다. 문제 출력시 소수점 4자리까지 표현하는데, 5자리에 반올림합니다.
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE STATION (
      ID INT AUTO_INCREMENT PRIMARY KEY,
      CITY VARCHAR(21),
      STATE CHAR(2),
      LAT_N DECIMAL(9,6),
      LONG_W DECIMAL(9,6)
  );

  INSERT INTO STATION (CITY, STATE, LAT_N, LONG_W) VALUES
  ('CityName1', 'CA', 34.052235, -118.243683),
  ('CityName2', 'TX', 29.760427, -95.369803),
  ('CityName3', 'NY', 40.712776, -74.005974),
  ('CityName4', 'FL', 25.761681, -80.191788),
  ('CityName5', 'IL', 41.878113, -87.629799);
  ```
  ```jsx
  [ 정답 ]
  SELECT ROUND(ABS(MIN(LAT_N) - MAX(LAT_N)) + ABS(MIN(LONG_W) - MAX(LONG_W)),4)
  FROM STATION
  ```
  - **해설 :** MIN, MAX함수를 사용해 최소값과 최대값을 구하고, ABS 함수를 사용해 절대값을 가져와 더한다음 ROUND함수를 사용해 소수점 4자리까지 반올림하여 표현합니다.
