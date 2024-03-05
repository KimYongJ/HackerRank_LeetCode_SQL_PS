- **SQL Project Planning**

  - [https://www.hackerrank.com/challenges/sql-projects/problem?isFullScreen=true](https://www.hackerrank.com/challenges/sql-projects/problem?isFullScreen=true)
  - 문제 : Projects 테이블의 Start_Date와 End_Date는 차이가 1씩 납니다. 이 때 특정 프로젝트의 종료날과 다른 프로젝트의 시작날이 같은 프로젝트는 하나의 프로젝트로 봅니다. 이렇게 하나로 볼 수 있는 프로젝트의 개수를 알고 싶습니다. 출력은 같은 프로젝트의 개수가 가장 많은 순대로 오름 차순 정렬하고, 프로젝트의 맨 처음 시작일과 가장 끝일자를 출력하는 문제입니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Projects (
      Task_ID INT,
      Start_Date DATE,
      End_Date DATE
  );

  INSERT INTO Projects (Task_ID, Start_Date, End_Date) VALUES
  (1, '2015-10-01', '2015-10-02'),
  (2, '2015-10-02', '2015-10-03'),
  (3, '2015-10-03', '2015-10-04'),
  (4, '2015-10-13', '2015-10-14'),
  (5, '2015-10-14', '2015-10-15'),
  (6, '2015-10-28', '2015-10-29'),
  (7, '2015-10-30', '2015-10-31');
  ```

  ```jsx
  [ 정답 ]
  SELECT MIN(START_DATE) START_DATE
  ,      MAX(END_DATE) END_DATE
  FROM (
          SELECT
          START_DATE ,
          END_DATE,
          END_DATE - ROW_NUMBER() OVER(ORDER BY START_DATE) AS DIFF
          FROM PROJECTS
  )PROJECT
  GROUP BY DIFF
  ORDER BY COUNT(*)
  ```

  - **해설 :** 이 문제를 해결하기 위해서는 먼저 같은 프로젝트라는 것을 알게 해주는 컬럼을 만들어야 합니다. 이 방법만 알면 간단히 해결 가능합니다. 문제 조건에서 날짜의 차이는 1씩 난다고 하였으므로 START_DATE기준으로 오름 차순 정렬 후 행의 순번대로 END_DATE과 빼주면 같은 프로젝트라면 같은 값을 갖게 됩니다. 아래 사진은 가운데 쿼리의 출력 결과 입니다.
   ![사진1](https://github.com/KimYongJ/SQL_ps/assets/106525587/d6d5e8ae-33b2-4044-b268-f22c35765ca8)

    보는 바와 같이 날짜형에 숫자를 빼면 숫자형으로 결과가 출력됩니다.
    같은 프로젝트의 컬럼을 구했으니 GROUP BY 키워드로 그룹을 지어 각 그룹당 가장 작은 START_DATE과 가장 큰 END_DATE을 구하면됩니다. 문제 조건에서 같은 프로젝트의 수가 많은 순으로 오름차순 하라고 하였으므로 COUNT(\*)을 ORDER BY절에 적어줍니다. ASC는 생략 가능합니다.
