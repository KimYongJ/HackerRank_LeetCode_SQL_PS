- population-density-difference
  - [https://www.hackerrank.com/challenges/population-density-difference/problem?isFullScreen=true](https://www.hackerrank.com/challenges/population-density-difference/problem?isFullScreen=true)
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
  (2, 'San Diego', 'USA', 'California', 1417946),
  (3, 'San Jose', 'USA', 'California', 1026908),
  (4, 'San Francisco', 'USA', 'California', 883305),
  (5, 'Fresno', 'USA', 'California', 530093);
  ```
  - **문제 :** CITY 테이블에서 최대 인구와 최소 인구의 차이를 출력합니다.
  ```jsx
  [ 정답 ]
  SELECT MAX(Population) - MIN(Population) AS POP
  FROM CITY
  ```
