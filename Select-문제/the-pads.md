- the-pads
  - [https://www.hackerrank.com/challenges/the-pads/problem?isFullScreen=true](https://www.hackerrank.com/challenges/the-pads/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE OCCUPATIONS (
      Name VARCHAR(100),
      Occupation VARCHAR(100)
  );
  INSERT INTO OCCUPATIONS (Name, Occupation) VALUES
  ('Ashely', 'Professor'),
  ('Christeen', 'Professor'),
  ('Jane', 'Actor'),
  ('Jenny', 'Doctor'),
  ('Julia', 'Actor'),
  ('Ketty', 'Professor'),
  ('Maria', 'Actor'),
  ('Meera', 'Singer'),
  ('Priya', 'Singer'),
  ('Samantha', 'Doctor');
  ```
  - **문제 :** OCCUPATIONS 테이블에서 NAME컬럼 옆에 괄호를 붙이고, 그안에 Occupation컬럼의 첫글자를 넣습니다. 그리고 가장 마지막에는 Occupation컬럼 별로 몇명인지 출력하는데 Occupation컬럼 뒤에 소문자 s와 닷(.)을 붙여서 `There are a total of 2 doctors.` 형태로 만들어 출력합니다. 이 때 마지막 There로 시작하는 문자 출력시 오름차순으로 정렬해 출력해야 합니다. 또한 Occupation 컬럼은 소문자로 출력해야 합니다.
  ```jsx
  [ 예시 출력 ]
  Ashely(P)
  Christeen(P)
  Jane(A)
  Jenny(D)
  Julia(A)
  Ketty(P)
  Maria(A)
  Meera(S)
  Priya(S)
  Samantha(D)
  There are a total of 2 doctors.
  There are a total of 2 singers.
  There are a total of 3 actors.
  There are a total of 3 professors.
  ```
  ```jsx
  [ 정답 ]
  SELECT NAME
  FROM (
          SELECT     CONCAT_WS('',NAME, '(', SUBSTR(Occupation,1,1) ,')') AS NAME
          FROM OCCUPATIONS
  ) A
  UNION ALL
  SELECT NAME
  FROM (
      SELECT     CONCAT_WS('','There are a total of ',CNT,' ', LOWER(Occupation),'s.') AS NAME
      ,        CNT
      from (
              SELECT COUNT(1) CNT
              ,      Occupation
              FROM OCCUPATIONS
              GROUP BY Occupation
      )OCCUPATIONS
  )B
  ORDER BY NAME
  ```
  - **해설 :** UNION ALL로 별개의 테이블 결과를 하나로 합쳐줍니다.
    - **CONCAT_WS :** 이 함수는 함수안의 인자들을 모두 합쳐줍니다. 단 첫번째 인자로 전달되는 것은 문자를 합칠 때마다 넣어 줍니다. 이 문제에서는 문자를 합칠 때 그 사이에 넣을 문자가 없기 때문에 빈칸(’’)으로 전달했습니다.
    - **영어 구문 출력 쿼리 :** Occupation 컬럼 별로 몇개가 있는지 그룹을 지어야 하기 때문에 Occupation 컬럼으로 그룹을 짓고 COUNT 함수로 컬럼 개수를 각각 출력 합니다. 그 후 CONCAT_WS 함수를 사용해 문자를 붙여 주며 문자를 붙일 때 출력 형식에 맞게 알맞는 알파벳을 적고, Occupation 컬럼은 소문자로 만들어 하나의 글자로 붙입니다.
