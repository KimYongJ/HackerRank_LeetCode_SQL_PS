# **Replace-Employee-ID-With-The-Unique-Identifier**

- [https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/)
- **문제 :** EMPLYEES테이블의 ID 별로 유니크 아이디를 출력하는 문제입니다. 이 때 유니크 아이디가 없다면 NULL을 출력해야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Employees (
  id INT,
  name VARCHAR(255),
  PRIMARY KEY (id)
);
CREATE TABLE EmployeeUNI (
  id INT,
  unique_id INT,
  PRIMARY KEY (id, unique_id)
);
INSERT INTO Employees (id, name) VALUES
(1, 'Alice'),
(7, 'Bob'),
(11, 'Meir'),
(9, 'Winston'),
(3, 'Jonathan');
INSERT INTO EmployeeUNI (id, unique_id) VALUES
(3, 1),
(11, 2),
(9, 3);
```

```jsx
[ 정답 ]
SELECT  UNI.UNIQUE_ID
,       EMP.NAME
FROM EMPLOYEES EMP
LEFT OUTER JOIN EMPLOYEEUNI UNI
    ON UNI.ID   =   EMP.ID
```

- **해설 :** 유니크 아이디가 없는 경우 NULL을 출력해야 하기 때문에 OUTER JOIN을 사용합니다. INNER JOIN 사용시 NULL인 경우 행이 줄어들기 때문에 문제의 조건을 만족할 수 없습니다.
