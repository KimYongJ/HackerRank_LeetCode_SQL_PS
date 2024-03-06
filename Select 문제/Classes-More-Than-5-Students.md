- **Classes More Than 5 Students**
  - [https://leetcode.com/problems/classes-more-than-5-students/](https://leetcode.com/problems/classes-more-than-5-students/)
  - **문제 :** COURSES 테이블에서 5명 이상의 STUDENT를 갖고 있는 CLASS 컬럼을 출력하는 문제 입니다.
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Courses (
      student VARCHAR(50),
      class VARCHAR(50),
      PRIMARY KEY (student, class)
  );
  INSERT INTO Courses (student, class) VALUES
  ('A', 'Math'),
  ('B', 'English'),
  ('C', 'Math'),
  ('D', 'Biology'),
  ('E', 'Math'),
  ('F', 'Computer'),
  ('G', 'Math'),
  ('H', 'Math'),
  ('I', 'Math');
  ```
  ```jsx
  [ 정답 ]
  SELECT CLASS
  FROM COURSES
  GROUP BY CLASS
  HAVING COUNT(*) >= 5
  ```
