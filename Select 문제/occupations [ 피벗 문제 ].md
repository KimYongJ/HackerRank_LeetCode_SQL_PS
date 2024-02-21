- occupations [ 피벗 문제 ]
  - [https://www.hackerrank.com/challenges/occupations/problem?isFullScreen=true](https://www.hackerrank.com/challenges/occupations/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE OCCUPATIONS (
      Name VARCHAR(100),
      Occupation VARCHAR(100)
  );

  INSERT INTO OCCUPATIONS (Name, Occupation) VALUES
  ('Samantha', 'Doctor'),
  ('Julia', 'Actor'),
  ('Maria', 'Actor'),
  ('Meera', 'Singer'),
  ('Ashely', 'Professor'),
  ('Ketty', 'Professor'),
  ('Christeen', 'Professor'),
  ('Jane', 'Actor'),
  ('Jenny', 'Doctor'),
  ('Priya', 'Singer');
  ```
  - **문제 :** Occupation 별로 이름을 세로로 출력합니다. 이 때 Occupation 순서는 Doctor, Professor, Singer, Actor 순서로 출력하며 이름은 오름차순으로 출력하고 값이 없을 경우 NULL을 출력합니다.
  - **출력 예시**
  | Doctor   | Professor | Singer | Actor |
  | -------- | --------- | ------ | ----- |
  | enny     | Ashely    | Meera  | Jane  |
  | Samantha | Christeen | Priya  | Julia |
  | NULL     | Ketty     | NULL   | Maria |
  ```jsx
  [ 정답 ]
  SELECT
  		MAX(Doctor) AS Doctor
  ,		MAX(Professor) AS Professor
  ,		MAX(Singer) AS Singer
  ,		MAX(Actor) AS Actor
  FROM(
  		SELECT
  				CASE WHEN Occupation = 'Doctor' THEN NAME ELSE NULL END Doctor
  		,		CASE WHEN Occupation = 'Professor' THEN NAME ELSE NULL END Professor
  		,		CASE WHEN Occupation = 'Singer' THEN NAME ELSE NULL END Singer
  		,		CASE WHEN Occupation = 'Actor' THEN NAME ELSE NULL END Actor
  		,		RN
  		FROM(
  				SELECT *
  				,		ROW_NUMBER() OVER(PARTITION BY Occupation ORDER BY NAME) RN
  				FROM occupations
  		)A
  		GROUP BY Occupation , NAME , RN
  )A
  GROUP BY RN
  ```
  - **해설 :** 먼저 가로로 출력하기 위해 가장 안쪽 쿼리에서 Occupation 컬럼을 그룹핑하고 NAME을 오름차순으로 하여 ROW_NUMBER 함수를 사용해 행에 순번을 지정합니다. 그리고 가운데 쿼리에서 CASE WHEN 구문을 사용해 Doctor, Professor, Singer, Actor 순으로 값을 출력해줍니다. 중간 쿼리를 따로 실행해보면 아래 사진과 같이 출력되는 것을 볼 수 있습니다.
    사진(1)
    이렇게 출력되고 나면 이제 단순히 RN을 깆준으로 GROUP을 묶어서 MAX로 출력해주면 잘 출력이 되는 것을 확인할 수 있습니다. 문제 조건에서 빈칸은 NULL을 출력하라고 했는데, MAX함수를 사용했을 때 값이 없다면 자동으로 NULL을 출력해줍니다.
