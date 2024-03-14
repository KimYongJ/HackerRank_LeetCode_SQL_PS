# **Calculate-Special-Bonus**

- [https://leetcode.com/problems/calculate-special-bonus/](https://leetcode.com/problems/calculate-special-bonus/)
- **문제 :** 각 직원에게 특별 보너스를 계산하는 문제입니다. 직원의 보너스는 해당 직원의 ID가 홀수이고, 이름이 'M'으로 시작하지 않는 경우 기본 급여의 100%입니다. 그 외의 경우에는 보너스가 없습니다(즉, 0입니다). 결과는 **employee_id**로 정렬하여 반환해야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Employees (
    employee_id INT,
    name VARCHAR(100),
    salary INT
);
INSERT INTO Employees (employee_id, name, salary) VALUES
(1, 'Meir', 30000),
(2, 'Michael', 3800),
(3, 'Addilyn', 7400),
(7, 'Juan', 6100),
(8, 'Kannon', 7700);
```

```jsx
[ 정답 ]
SELECT  EMPLOYEE_ID
,       CASE WHEN EMPLOYEE_ID%2=1 AND SUBSTR(NAME,1,1) !='M' THEN SALARY ELSE 0 END BONUS
FROM EMPLOYEES
ORDER BY EMPLOYEE_ID
```

- **해설 :** EMPLOYEE_ID가 홀수이고, NAME의 첫글자가 M이 아닌 것을 구해야하는 문제입니다. 나머지 연산과, SUBSTR 함수를 사용해 문제를 해결하였습니다.
