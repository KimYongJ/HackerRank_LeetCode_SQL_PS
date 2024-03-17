# **Find-Total-Time-Spent-by-Each-Employee**

- [https://leetcode.com/problems/find-total-time-spent-by-each-employee/](https://leetcode.com/problems/find-total-time-spent-by-each-employee/)
- **문제 :** EMPLOYEES 테이블에서 각 직원이 날짜별로 사무실에 있었던 시간을 출력하는 문제입니다. 사무실에 있었던 시간은 OUT_TIME - IN_TIME으로 구합니다

```jsx
[ 문제 조건 ]
CREATE TABLE Employees (
    emp_id int,
    event_day date,
    in_time int,
    out_time int
);
INSERT INTO Employees (emp_id, event_day, in_time, out_time) VALUES
(1, '2020-11-28', 4, 32),
(1, '2020-11-28', 55, 420),
(1, '2020-12-03', 1, 43),
(1, '2020-12-03', 3, 33),
(2, '2020-12-09', 47, 74);
```

```jsx
[ 정답 ]
SELECT  EVENT_DAY AS DAY
,       EMP_ID
,       SUM(OUT_TIME - IN_TIME) AS TOTAL_TIME
FROM EMPLOYEES
GROUP BY EMP_ID, EVENT_DAY
```

- **해설 :** EMP_ID와 EVENT_DAY를 기준으로 그룹을 묶어 SUM키워드에 사무실에 있었던 시간을 넣어 줍니다.
