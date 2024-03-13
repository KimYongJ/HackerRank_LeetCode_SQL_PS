# **The-Number-of-Employees-Which-Report-to Each-Employee**

- [https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/](https://leetcode.com/problems/the-number-of-employees-which-report-to-each-employee/)
- **문제 :** 각 직원에게 직접 보고하는 직원의 수와 각 관리자에게 보고하는 직원의 평균 나이를 계산하는 문제입니다. '직원' 테이블에는 직원의 ID, 이름, 상사의 ID, 나이 정보가 들어 있습니다. 상사에게 보고하는 직원이 한 명 이상 있는 사람을 '관리자'로 간주합니다. 관리자의 ID와 이름, 그리고 그에게 직접 보고하는 직원 수와 그 직원들의 평균 나이를 반올림하여 정수로 표시해야 합니다. 결과는 직원 ID 순으로 정렬되어 반환되어야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Employees (
    employee_id int,
    name varchar(255),
    reports_to int,
    age int
);
INSERT INTO Employees (employee_id, name, reports_to, age) VALUES
(9, 'Hercy', NULL, 43),
(6, 'Alice', 9, 41),
(4, 'Bob', 9, 36),
(2, 'Winston', NULL, 37);
```

```jsx
[ 정답 ]
SELECT  A.EMPLOYEE_ID
,       A.NAME
,       COUNT(B.REPORTS_TO) REPORTS_COUNT
,       ROUND(AVG(B.AGE)) AS AVERAGE_AGE
FROM EMPLOYEES A
LEFT OUTER JOIN EMPLOYEES B
    ON A.EMPLOYEE_ID = B.REPORTS_TO
GROUP BY A.EMPLOYEE_ID , A.NAME
HAVING REPORTS_COUNT >= 1
ORDER BY A.EMPLOYEE_ID
```

- **해설 :** 상사에게 보고하는 직원을 고르기 위해 조인조건절을 아래와 같이 했습니다.
  - ON A.EMPLOYEE_ID = B.REPORTS_TO
  그 후 그룹을 지어 보고하는 인원의 수와 평균나이를 계산합니다. 문제에서 보고하는 인원이 1명이상인 경우 출력을 요청했기 때문에 HAVING 절에 조건을 추가해주었습니다.
