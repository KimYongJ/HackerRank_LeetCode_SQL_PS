- weather-observation-station-19

  - [https://www.hackerrank.com/challenges/weather-observation-station-19/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-19/problem?isFullScreen=true)
  - **문제 :** 두점 P1(a,b) , P2(c,d)사이의 유클리드 거리를 구하는 것입니다. a,b는 LAT_N 컬럼 값의 최소값, 최대값이며 c,d는 LONG_W 컬럼값의 최소값 최대값입니다. 유클리드 거리 출력시 소수점 4자리까지 표현하며 5자리에서 반올림합니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE STATION (
      ID INT AUTO_INCREMENT PRIMARY KEY,
      CITY VARCHAR(21),
      STATE CHAR(2),
      LAT_N FLOAT,
      LONG_W FLOAT
  );

  INSERT INTO STATION (CITY, STATE, LAT_N, LONG_W) VALUES
  ('Seoul', 'SE', 37.5665, 126.9780),
  ('New York', 'NY', 40.7128, -74.0060),
  ('Los Angeles', 'CA', 34.0522, -118.2437),
  ('London', 'LD', 51.5074, -0.1278),
  ('Beijing', 'BJ', 39.9042, 116.4074),
  ('Tokyo', 'TK', 35.6895, 139.6917),
  ('Sydney', 'SD', -33.8688, 151.2093),
  ('Paris', 'PR', 48.8566, 2.3522),
  ('Berlin', 'BL', 52.5200, 13.4050),
  ('Moscow', 'MC', 55.7558, 37.6173);
  ```

  ```jsx
  [ 정답 ]
  SELECT ROUND(
                  SQRT(
                          POW(MIN(LAT_N)-MAX(LAT_N),2)+ POW(MIN(LONG_W)-MAX(LONG_W),2)
                      )
              ,4)
  FROM STATION
  ```

  - **해설 :** 유클리드 거리를 구하는 공식을 씁니다. 이 과정에서 POW함수는 첫번 째인자를 두번째 인자만큼 제곱하는 것으로 2를 전달하여 제곱이 되도록하였습니다. 또한 제곱근을 구하기 위한 함수로 SQRT함수를 사용해 제곱근을 구하고, ROUND함수를 사용해 소수점 5자리에서 반올림해 4자리를 표현했습니다.
