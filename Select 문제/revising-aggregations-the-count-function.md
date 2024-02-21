- revising-aggregations-the-count-function
  - [https://www.hackerrank.com/challenges/revising-aggregations-the-count-function/problem?isFullScreen=true](https://www.hackerrank.com/challenges/revising-aggregations-the-count-function/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE CITY (
      ID INT PRIMARY KEY,
      Name VARCHAR(100),
      CountryCode CHAR(3),
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
  - **문제 :** CITY 테이블에서 Population이 10만 보다 큰 도시의 개수를 세는 문제입니다.
  ```jsx
  [ 정답 ]
  SELECT COUNT(1) AS CNT
  FROM city
  WHERE Population > 100000
  ```
