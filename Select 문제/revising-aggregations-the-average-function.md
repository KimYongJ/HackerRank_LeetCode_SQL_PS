- revising-aggregations-the-average-function
  - [https://www.hackerrank.com/challenges/revising-aggregations-the-average-function/problem?isFullScreen=true](https://www.hackerrank.com/challenges/revising-aggregations-the-average-function/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE CITY (
      ID INT PRIMARY KEY,
      Name VARCHAR(100),
      CountryCode VARCHAR(3),
      District VARCHAR(100),
      Population INT
  );
  INSERT INTO CITY (ID, Name, CountryCode, District, Population) VALUES
  (1, 'Los Angeles', 'USA', 'California', 3971883),
  (2, 'San Diego', 'USA', 'California', 1406630),
  (3, 'San Jose', 'USA', 'California', 1026908);
  ```
  - **문제 :** CITY 테입블에서 District 값이 'California' 곳의 평균 인구를 출력합니다.
  ```jsx
  [ 정답 ]
  SELECT AVG(POPULATION)
  FROM CITY
  WHERE DISTRICT = 'CALIFORNIA'
  ```
