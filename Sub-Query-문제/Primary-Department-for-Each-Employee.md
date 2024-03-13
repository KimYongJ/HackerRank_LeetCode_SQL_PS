# **Primary-Department-for-Each-Employee**

- [https://leetcode.com/problems/primary-department-for-each-employee/](https://leetcode.com/problems/primary-department-for-each-employee/)
- **문제 :** 각 직원에 대해 그들의 기본 부서를 보고하는 SQL 쿼리를 작성해야 합니다. **Employee** 테이블에는 직원 ID, 부서 ID, 그리고 해당 부서가 기본 부서인지 여부를 나타내는 플래그가 있습니다. 기본 부서로 표시된 부서('Y')만을 결과로 보여주어야 하며, 직원이 여러 부서에 속해있는 경우에도 단 한 개의 기본 부서만을 리포트해야 합니다. 결과는 어떤 순서로 반환해도 괜찮습니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Employee (
    employee_id int,
    department_id varchar(4),
    primary_flag enum('Y', 'N')
);
INSERT INTO Employee (employee_id, department_id, primary_flag) VALUES
(1, '1', 'N'),
(2, '1', 'Y'),
(2, '2', 'N'),
(3, '2', 'N'),
(4, '2', 'N'),
(4, '3', 'Y'),
(4, '4', 'N');
```

```jsx
[ 정답(1) ]
SELECT DISTINCT *
FROM(
		SELECT	EMPLOYEE_ID
		,		MAX(DEPARTMENT_ID) DEPARTMENT_ID
		FROM employee
		GROUP BY EMPLOYEE_ID
		HAVING COUNT(EMPLOYEE_ID) = 1
		UNION
		SELECT	EMPLOYEE_ID
		,		DEPARTMENT_ID
		FROM employee
		WHERE PRIMARY_FLAG = 'Y'
)TEMP

[ 정답(2) ]
SELECT	EMPLOYEE_ID
,		DEPARTMENT_ID
FROM employee
WHERE PRIMARY_FLAG = 'Y'
OR EMPLOYEE_ID IN(
					SELECT	EMPLOYEE_ID
					FROM employee
					GROUP BY EMPLOYEE_ID
					HAVING COUNT(EMPLOYEE_ID) = 1
				)
```

- **정답 (1) 해설 :** UNION을 사용해 부서가 하나만있는 사원과 고유플레그 값이 Y인 것을 합쳐 줍니다. 위 방법으로 문제를 풀면 중복 제거가 필수기 때문에 DISTINCT 키워드를 사용했습니다.
- **정답 (2) 해설 :** 정답(1)과 비슷하지만 UNION을 사용하지 않고 그룹핑한 SELECT 쿼리만 IN절로 내린 쿼리입니다. 고유플레그 값이 Y이거나, 서브쿼리의 EMPLOYEE_ID 값이 같을 때 출력해줍니다.
