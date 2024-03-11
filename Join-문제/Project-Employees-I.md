# **Project-Employees-I**

- [https://leetcode.com/problems/project-employees-i/](https://leetcode.com/problems/project-employees-i/)
- **문제 :** PROJECT_ID 별로 EXPERIENCE_YEARS의 평균을 소수점 2자리 까지 반올림하여 표현합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Employee (
  employee_id INT,
  name VARCHAR(255),
  experience_years INT
);
CREATE TABLE Project (
  project_id INT,
  employee_id INT,
  PRIMARY KEY (project_id, employee_id)
);
INSERT INTO Employee (employee_id, name, experience_years) VALUES
(1, 'Khaled', 3),
(2, 'Ali', 2),
(3, 'John', 1),
(4, 'Doe', 2);
INSERT INTO Project (project_id, employee_id) VALUES
(1, 1),
(1, 2),
(1, 3),
(2, 1),
(2, 4);
```

```jsx
[ 정답 ]
SELECT  PJ.PROJECT_ID
,       ROUND(AVG(EMP.EXPERIENCE_YEARS),2) AVERAGE_YEARS
FROM PROJECT PJ
LEFT OUTER JOIN EMPLOYEE EMP
        ON EMP.EMPLOYEE_ID  =   PJ.EMPLOYEE_ID
GROUP BY PJ.PROJECT_ID
```

- **해설 :** 문제 요청대로 프로젝트 아이디를 그룹화한 후 AVG 함수로 평균을 구하고, ROUND 함수로 소수점 2자리까지 표현하는데 3자리에서 반올림합니다.
