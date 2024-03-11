# **Students-and-Examinations**

- [https://leetcode.com/problems/students-and-examinations/](https://leetcode.com/problems/students-and-examinations/)
- **문제 :** 학생별로 각 과목의 시험에 몇번 응시했는지를 표시하면 됩니다. 이 때 응시하지 않은 과목도 출력해야 합니다. 응시하지 않은 경우는 0으로 출력됩니다. 출력시 STUDENT_ID와 SUBJECT_NAME으로 오름차순 정렬합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Students (
  student_id INT PRIMARY KEY,
  student_name VARCHAR(50)
);
CREATE TABLE Subjects (
  subject_name VARCHAR(50) PRIMARY KEY
);
CREATE TABLE Examinations (
  student_id INT,
  subject_name VARCHAR(50),
  FOREIGN KEY (student_id) REFERENCES Students(student_id),
  FOREIGN KEY (subject_name) REFERENCES Subjects(subject_name)
);
INSERT INTO Students (student_id, student_name) VALUES
(1, 'Alice'),
(2, 'Bob'),
(13, 'John'),
(6, 'Alex');
INSERT INTO Subjects (subject_name) VALUES
('Math'),
('Physics'),
('Programming');
INSERT INTO Examinations (student_id, subject_name) VALUES
(1, 'Math'),
(1, 'Physics'),
(1, 'Programming'),
(1, 'Physics'),
(1, 'Math'),
(13, 'Math'),
(13, 'Programming'),
(13, 'Physics'),
(2, 'Math'),
(2, 'Programming'),
(1, 'Math');
```

```jsx
[ 정답 ]
SELECT	ST.STUDENT_ID
,		ST.STUDENT_NAME
,		ST.SUBJECT_NAME
,		COUNT(EX.SUBJECT_NAME) AS ATTENDED_EXAMS
FROM (
		SELECT	*
		FROM STUDENTS ST
		CROSS JOIN SUBJECTS SB
)ST
LEFT OUTER JOIN EXAMINATIONS EX
	ON EX.STUDENT_ID	=	ST.STUDENT_ID
	AND EX.SUBJECT_NAME	=	ST.SUBJECT_NAME
GROUP BY ST.STUDENT_ID, ST.STUDENT_NAME, ST.SUBJECT_NAME
ORDER BY ST.STUDENT_ID,	ST.SUBJECT_NAME
```

- **해설 :** 각 학생이 특정 과목에 응시하지 않았을 수도 있습니다. 응시하지 않은 학생에 대해서도 과목에 대해 출력해줘야 하기 때문에 먼저 각 학생과 과목을 맵핑 시키는 작업이 필요합니다. 이를 위해 두 테이블을 CROSS JOIN합니다. CROSS JOIN은 두 테이블 행 하나마다 서로 결합 하기 때문에 학생마다 모든 과목이 맵핑됩니다. CROSS JOIN 후 실행 결과는 아래 사진과 같습니다
  
  ![사진1](https://github.com/KimYongJ/HackerRank_LeetCode_SQL_PS/assets/106525587/4f02f54b-4ec9-4891-b2f6-41861e347391)

- 그 후 EXAMINATIONS 테이블을 조인하고, 출력해야 하는 컬럼들을 그룹화 한 후 COUNT 함수를 사용해 과목의 숫자를 카운팅합니다. 이 때 COUNT 함수 안에 들어가는 컬럼은 EXAMINATIONS 테이블의 SUBJECT_NAME 컬럼이여야만 합니다. NULL인 경우 카운팅을 제거해줘야 하기 때문입니다. 예를 들어 ST.SUBJECT_NAME을 넣는다면, 해당 컬럼의 값은 항상 있기 때문에 응시하지 않아도 결과가 1로 나옵니다. COUNT함수는 행 수를 계산할 때 NULL 값을 제외 합니다. 그렇기에 NULL일 수 있는 컬럼인 EX.SUBJECT_NAME을 안에 적어주어야 합니다.
