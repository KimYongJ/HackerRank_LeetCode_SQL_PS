- **Big-Countries**
  - [https://leetcode.com/problems/big-countries/](https://leetcode.com/problems/big-countries/)
  - **문제 :** WORLD 테이블에서 AREA 컬럼이 3,000,000 이상 이거나, POPULATION 컬럼이 25,000,000 이상인 행들의 NAME, POPULATION, AREA를 출력합니다.
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE World (
      name VARCHAR(50),
      continent VARCHAR(50),
      area INT,
      population INT,
      gdp BIGINT
  );
  INSERT INTO World (name, continent, area, population, gdp) VALUES
  ('Afghanistan', 'Asia', 652230, 25500100, 20343000000),
  ('Albania', 'Europe', 28748, 2831741, 12960000000),
  ('Algeria', 'Africa', 2381741, 37100000, 188681000000),
  ('Andorra', 'Europe', 468, 78115, 3712000000),
  ('Angola', 'Africa', 1246700, 20609294, 100990000000);
  ```
  ```jsx
  [ 정답 ]
  SELECT NAME, POPULATION, AREA
  FROM WORLD
  WHERE AREA >= 3000000 OR POPULATION >=25000000
  ```
