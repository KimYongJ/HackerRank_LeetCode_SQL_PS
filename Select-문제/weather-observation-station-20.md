- weather-observation-station-20
  - [https://www.hackerrank.com/challenges/weather-observation-station-20/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-20/problem?isFullScreen=true)
  - **문제 :** STATION 테이블에서 LAT_N 컬럼을 정렬했을 때 LAT_N 컬럼의 중앙 값을 구하는 문제입니다. 테이블 컬럼이 짝수 일때는 고려하지 않고 문제를 풉니다.
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE STATION (
      ID INT,
      CITY VARCHAR(21),
      STATE VARCHAR(2),
      LAT_N DECIMAL(10, 4),
      LONG_W DECIMAL(10, 4)
  );
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES (1, 'City1', 'ST', 10.1234, -20.5678);
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES (2, 'City2', 'ST', 20.2468, -41.1356);
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES (3, 'City3', 'ST', 30.3702, -61.7034);
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES (4, 'City4', 'ST', 40.4936, -82.2712);
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES (5, 'City5', 'ST', 50.6170, -102.8390);
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES (6, 'City6', 'ST', 60.7404, -123.4068);
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES (7, 'City7', 'ST', 70.8638, -143.9746);
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES (8, 'City8', 'ST', 80.9872, -164.5424);
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES (9, 'City9', 'ST', 91.1106, -185.1102);
  INSERT INTO STATION (ID, CITY, STATE, LAT_N, LONG_W) VALUES (10, 'City10', 'ST', 101.2340, -205.6780);
  ```
  ```jsx
  [ 정답 ]
  SELECT ROUND(AVG(LAT_N),4) -- AVG함수를 쓰지 않아도 AC입니다.
  FROM (
          SELECT     PERCENT_RANK() OVER(ORDER BY LAT_N) PRNK
          ,        LAT_N
          FROM STATION
  )STATION
  WHERE PRNK = 0.5
  ```
  - **해설 : PERCENT_RANK()** 함수를 사용해 순위를 구해옵니다. **PERCENT_RANK** 함수는 순위를 0부터 1사이의 숫자로 표현합니다. 홀수 행일 때 중앙 값은 정확히 0.5가 됩니다. 그러나 짝수행일 때 중앙 값은 정확히 0.5가 아닙니다. 12행이 있다고 했을 때 6번째 행은 0.4545 , 7번째 행은 0.5454 입니다. 그래서 이 문제를 풀 때 짝수 행일 경우도 고려해서 문제를 푼다면 답이 달라져야 한다 생각됩니다(짝수 행일 때 0.5를 대입하면 NULL이 나오기 때문이죠) 문제를 풀 때는 홀수 행인 경우만 고려해 0.5를 대입하여 AC를 받았습니다.
