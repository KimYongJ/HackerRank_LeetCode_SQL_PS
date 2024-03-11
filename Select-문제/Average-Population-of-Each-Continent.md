- Average Population of Each Continent
  - [https://www.hackerrank.com/challenges/average-population-of-each-continent/problem?isFullScreen=true](https://www.hackerrank.com/challenges/average-population-of-each-continent/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE COUNTRY (
      Code VARCHAR(3) PRIMARY KEY,
      Name VARCHAR(100),
      Continent VARCHAR(50),
      Population INT
  );
  CREATE TABLE CITY (
      ID INT PRIMARY KEY,
      Name VARCHAR(100),
      CountryCode VARCHAR(3),
      District VARCHAR(100),
      Population INT,
      FOREIGN KEY (CountryCode) REFERENCES COUNTRY(Code)
  );
  INSERT INTO COUNTRY (Code, Name, Continent, Population) VALUES
  ('EGY', 'Egypt', 'Africa', 102334404),
  ('NGA', 'Nigeria', 'Africa', 206139589),
  ('ZAF', 'South Africa', 'Africa', 59308690),
  ('USA', 'United States', 'North America', 331002651),
  ('JPN', 'Japan', 'Asia', 126476461),
  ('BRA', 'Brazil', 'South America', 212559417);
  INSERT INTO CITY (ID, Name, CountryCode, District, Population) VALUES
  (1, 'Cairo', 'EGY', 'Cairo', 20000000),
  (2, 'Lagos', 'NGA', 'Lagos', 21000000),
  (3, 'Johannesburg', 'ZAF', 'Gauteng', 957441),
  (4, 'New York', 'USA', 'New York', 8175133),
  (5, 'Tokyo', 'JPN', 'Tokyo', 13929286),
  (6, 'Sao Paulo', 'BRA', 'Sao Paulo', 12325232);
  ```
  - **문제 :** 모든 대륙의 이름(COUNTRY.Continent)과 해당 대륙의 평균 도시 인구(CITY.Population)를 구합니다. 이 때 평균 도시 인구의 소수점은 내림해주세요
  ```jsx
  [ 정답 ]
  SELECT COUNTRY.Continent
  ,      FLOOR(AVG(CITY.Population)) AS POP
  FROM COUNTRY
  INNER JOIN CITY
  	ON CITY.CountryCode = COUNTRY.Code
  GROUP BY COUNTRY.Continent
  ```
