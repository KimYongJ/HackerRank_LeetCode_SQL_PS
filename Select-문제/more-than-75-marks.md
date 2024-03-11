- more-than-75-marks

  - [https://www.hackerrank.com/challenges/more-than-75-marks/problem?isFullScreen=true](https://www.hackerrank.com/challenges/more-than-75-marks/problem?isFullScreen=true)

  ```jsx
  [ 문제 조건 ]
  -- 테이블 생성
  CREATE TABLE students (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(255),
      marks INT
  );

  -- 값 삽입
  INSERT INTO students (name, marks) VALUES
  ('Ashley', 78),
  ('Julia', 85),
  ('Belvet', 92),
  ('Bobby', 65),
  ('Robby', 55);
  ```

  - **문제 :** marks가 75점 이상인 학생들의 이름을 출력하되, 이름 마지막 3글자를 기준으로 오름차순 정렬하고 3글자가 같다면 id기준으로 오름차순 정렬합니다.

  ```jsx
  [ 정답 ]
  select name
  from students
  where marks > 75
  order by RIGHT(name, 3), id
  ```

  - **해설 :** 마지막 3글자를 가져오기 위해 오른쪽 끝에서부터 원하는 길이만큼의 문자열을 직접적으로 추출할 수 있는 RIGHT 함수를 사용했습니다. 오름차순 정렬은 ASC인데, 생략 가능합니다.(default = asc)
