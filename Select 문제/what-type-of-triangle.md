- what-type-of-triangle
  - [https://www.hackerrank.com/challenges/what-type-of-triangle/problem?isFullScreen=true](https://www.hackerrank.com/challenges/what-type-of-triangle/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE TRIANGLES (
      A INT,
      B INT,
      C INT
  );
  INSERT INTO TRIANGLES (A, B, C) VALUES
  (2, 2, 3),  -- 이등변삼각형
  (3, 3, 3),  -- 등변삼각형
  (3, 4, 5),  -- 부등변삼각형
  (1, 2, 3);  -- 삼각형이 아님
  ```
  - **문제 :** 각 행마다 이등변 삼각형인지, 등변삼각형인지, 부등변삼각형인지, 삼각형이 아닌지 출력합니다.
  ```jsx
  [ 정답 ]
  SELECT
  CASE
  	WHEN A+B <= C OR A+C <=B OR B+C <=A THEN 'Not A Triangle'
  	WHEN A=B AND B=C THEN 'Equilateral'
  	WHEN A=B OR B=C OR A=C THEN 'Isosceles'
  	ELSE 'Scalene'
  END
  FROM TRIANGLES;
  ```
