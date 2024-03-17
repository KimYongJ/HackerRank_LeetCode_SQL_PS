- asian-population

  - [https://www.hackerrank.com/challenges/asian-population/problem?isFullScreen=true](https://www.hackerrank.com/challenges/asian-population/problem?isFullScreen=true)

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
  ('KOR', 'South Korea', 'Asia', 51780579),
  ('USA', 'United States', 'North America', 331002651),
  ('JPN', 'Japan', 'Asia', 126476461),
  ('IND', 'India', 'Asia', 1380004385),
  ('FRA', 'France', 'Europe', 65273511);

  INSERT INTO CITY (ID, Name, CountryCode, District, Population) VALUES
  (1, 'Seoul', 'KOR', 'Seoul', 9904312),
  (2, 'New York', 'USA', 'New York', 8175133),
  (3, 'Tokyo', 'JPN', 'Tokyo', 13929286),
  (4, 'Mumbai', 'IND', 'Maharashtra', 12442373),
  (5, 'Paris', 'FRA', 'Ile-de-France', 2148327);
  ```

  - **문제 :** CITY 테이블의 POPULATION의 합을 구하는데, COUNTRY 테이블의 CONTINENT 값이 ‘ASIA’인 것만 합을 구해야 합니다. 조인 조건은 다음과 같습니다
    - COUNTRY.CODE = CITY.COUNTRYCODE

  ```jsx
  [ 정답 ]
  SELECT SUM(CITY.POPULATION)
  FROM CITY
  INNER JOIN COUNTRY
      ON COUNTRY.CODE = CITY.COUNTRYCODE
  WHERE COUNTRY.CONTINENT = 'ASIA'
  ```
