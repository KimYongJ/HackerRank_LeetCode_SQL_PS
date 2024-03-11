- placements

  - [https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true](https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true)

  ```jsx
  [ 문제 조건 ]
  -- Students 테이블 생성
  CREATE TABLE Students (
      ID INT PRIMARY KEY,
      Name VARCHAR(100)
  );

  -- Friends 테이블 생성
  CREATE TABLE Friends (
      ID INT PRIMARY KEY,
      Friend_ID INT,
      FOREIGN KEY (ID) REFERENCES Students(ID),
      FOREIGN KEY (Friend_ID) REFERENCES Students(ID)
  );

  -- Packages 테이블 생성
  CREATE TABLE Packages (
      ID INT PRIMARY KEY,
      Salary DECIMAL(10,2),
      FOREIGN KEY (ID) REFERENCES Students(ID)
  );

  -- Students 테이블에 데이터 삽입
  INSERT INTO Students (ID, Name) VALUES
  (1, 'Ashley'),
  (2, 'Samantha'),
  (3, 'Julia'),
  (4, 'Scarlet');

  -- Friends 테이블에 데이터 삽입
  INSERT INTO Friends (ID, Friend_ID) VALUES
  (1, 2),
  (2, 3),
  (3, 4),
  (4, 1);

  -- Packages 테이블에 데이터 삽입
  INSERT INTO Packages (ID, Salary) VALUES
  (1, 15.20),
  (2, 10.06),
  (3, 11.55),
  (4, 12.12);
  ```

  - **문제 :** Students , Friends , Packages 테이블이 주어지고, 자신보다 높은 급여를 제안 받은 최고의 친구를 가진 학생들의 이름을 출력하는 쿼리를 작성합니다. 출력 결과는 최고의 친구가 제안받은 금액을 기준으로 오름차순 정렬합니다.

  ```jsx
  [ 정답 ]
  select st.name
  from Students st
  inner join packages pk1
          on pk1.id = st.id
  inner join friends fr
          on fr.id = st.id
  inner join packages pk2
          on pk2.id = fr.friend_id
  where pk1.salary < pk2.salary
  order by pk2.salary
  ```
