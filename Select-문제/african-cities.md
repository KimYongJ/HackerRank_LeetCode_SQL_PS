- african-cities
  - [https://www.hackerrank.com/challenges/african-cities/problem?isFullScreen=true](https://www.hackerrank.com/challenges/african-cities/problem?isFullScreen=true)
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
  ('JPN', 'Japan', 'Asia', 126476461);
  INSERT INTO CITY (ID, Name, CountryCode, District, Population) VALUES
  (1, 'Cairo', 'EGY', 'Cairo', 20000000),
  (2, 'Lagos', 'NGA', 'Lagos', 21000000),
  (3, 'Johannesburg', 'ZAF', 'Gauteng', 957441),
  (4, 'New York', 'USA', 'New York', 8175133),
  (5, 'Tokyo', 'JPN', 'Tokyo', 13929286);
  ```
  - **문제 :** CITY 테이블에서 NAME을 조회하는데, COUNTRY 테이블의 CONTINENT 컬럼이 'Africa' 인 값만 조회합니다. CITY 테이블과 COUNTRY 테이블의 조인 조건은 각각 CountryCode컬럼과 Code컬럼 입니다.
  ```jsx
  [ 정답 ]
  SELECT CITY.NAME
  FROM CITY
  INNER JOIN COUNTRY
      ON COUNTRY.CODE = CITY.COUNTRYCODE
  WHERE COUNTRY.CONTINENT = 'Africa'
  ```
