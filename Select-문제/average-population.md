- average-population
  - [https://www.hackerrank.com/challenges/average-population/problem?isFullScreen=true](https://www.hackerrank.com/challenges/average-population/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE CITY (
      ID INT PRIMARY KEY,
      Name VARCHAR(100),
      Country VARCHAR(100),
      District VARCHAR(100),
      Population INT
  );
  INSERT INTO CITY (ID, Name, Country, District, Population) VALUES
  (1, 'Seoul', 'South Korea', 'Seoul', 10000000),
  (2, 'New York', 'United States', 'New York', 8500000),
  (3, 'Tokyo', 'Japan', 'Tokyo', 9000000),
  (4, 'Mumbai', 'India', 'Maharashtra', 12000000),
  (5, 'Paris', 'France', 'Ile-de-France', 2200000);
  ```
  - **문제 :** city 테이블에서 Population 의 평균을 구하고, 소수점은 내림하여 구하는 문제 입니다.
  ```jsx
  [ 정답 ]
  select floor(avg(Population)) from city
  ```
