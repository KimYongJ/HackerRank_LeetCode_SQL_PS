- **Number-of-Unique-Subjects-Taught-by-Each-Teacher**

  - [https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/](https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/)
  - **문제 :** 교사별로 고유한 과목(SUBJECT_ID)수를 출력합니다. 과목(SUBJECT_ID)수는 CNT로 표현합니다.

  ```jsx
  [ 문제 조건 ]
  CREATE TABLE Teacher (
      teacher_id INT,
      subject_id INT,
      dept_id INT,
      PRIMARY KEY (subject_id, dept_id)
  );

  INSERT INTO Teacher (teacher_id, subject_id, dept_id) VALUES
  (1, 2, 3),
  (1, 2, 4),
  (1, 3, 3),
  (2, 1, 1),
  (2, 2, 1),
  (2, 3, 1),
  (2, 4, 1);
  ```

  ```jsx
  [ 정답(1) ]
  SELECT TEACHER_ID
  ,      COUNT(DISTINCT SUBJECT_ID) CNT
  FROM TEACHER
  GROUP BY TEACHER_ID

  [ 정답(2) ]
  SELECT 	TEACHER_ID
  ,		COUNT(*) CNT
  FROM(
  	SELECT TEACHER_ID
  	,      SUBJECT_ID
  	FROM TEACHER
  	GROUP BY TEACHER_ID, SUBJECT_ID
  )TC
  GROUP BY TEACHER_ID
  ```

  - **정답(1) 해설 :** 과목이 중복해서 있을 수 있기 때문에 DISTINCT 키워드를 사용합니다. COUNT안에서 DISTINCT가 사용될 경우 같은 SUBJECT_ID는 제거합니다.
  - **정답(2) 해설 :** 먼저 교사 아이디와 과목 아이디로 그룹 후 중복을 제거하고 다시 교사 아이디로 그룹을 지어 과목의 수를 출력합니다.
