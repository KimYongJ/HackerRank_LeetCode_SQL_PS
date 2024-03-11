- japan-population
  - [https://www.hackerrank.com/challenges/japan-population/problem?isFullScreen=true](https://www.hackerrank.com/challenges/japan-population/problem?isFullScreen=true)
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
  (1, 'Tokyo', 'JPN', 'Tokyo', 13929286),
  (2, 'Yokohama', 'JPN', 'Kanagawa', 3726167),
  (3, 'Osaka', 'JPN', 'Osaka', 2768454),
  (4, 'Nagoya', 'JPN', 'Aichi', 2295668),
  (5, 'Sapporo', 'JPN', 'Hokkaido', 1952356),
  (6, 'Fukuoka', 'JPN', 'Fukuoka', 1559392),
  (7, 'Kobe', 'JPN', 'Hyogo', 1530847),
  (8, 'Kyoto', 'JPN', 'Kyoto', 1474570);
  ```
  - **문제 :** 주어진 CITY 테이블을 사용하여, 일본(Japan)의 모든 도시 인구의 합계를 조회하세요. 일본의 COUNTRYCODE는 JPN입니다.
  ```jsx
  [ 정답 ]
  SELECT SUM(Population)
  FROM CITY
  WHERE CountryCode = 'JPN'
  ```
