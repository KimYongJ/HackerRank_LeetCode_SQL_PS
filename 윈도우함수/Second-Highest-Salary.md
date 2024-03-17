# **Second-Highest-Salary**

- [https://leetcode.com/problems/second-highest-salary/](https://leetcode.com/problems/second-highest-salary/)
- **문제**
  - "두 번째로 높은 급여 찾기"에 관한 SQL 문제입니다. 각 직원의 ID와 급여가 있는 `Employee` 테이블이 주어졌을 때, 두 번째로 높은 급여를 찾는 쿼리를 작성하는 것이 목적입니다. 만약 두 번째로 높은 급여가 없으면 (즉, 한 명의 직원만 있거나 모든 직원의 급여가 같을 경우) `NULL` 값을 반환해야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Employee (
    id INT, salary INT
);

[ version 1 ]
INSERT INTO Employee (id, salary) VALUES
(1, 100),(2, 200),(3, 300);

[ version 2 ]
INSERT INTO Employee (id, salary) VALUES
(1, 100);

[ version 3 ]
INSERT INTO Employee (id, salary) VALUES
(1, 100),(2, 100),(3, 50);
```

```jsx
[ 정답 ]
SELECT MAX(SALARY) SECONDHIGHESTSALARY
FROM(
		SELECT	SALARY
		,		DENSE_RANK() OVER(ORDER BY SALARY DESC) RNK
		FROM EMPLOYEE
)TEMP
WHERE RNK = 2;
```

- **해설**
  - 이 문제는 dense_rank를 사용해 문제를 해결했습니다. rank함수는 같은 급여가 2개 라면 그 행만큼 rank가 추가 됩니다(ex. 100 100 50 일때 등수는 1 1 2 가됨) 그런데 dense_rank는 같은 등 수 일 때 같은 순위를 주기 때문에 dense_rank가 이번 문제에 적합하다 생각합니다.
  - 또한 출력될 때 등수가 2등인 값이 없으면 NULL을 출력해야 합니다. 이를 위해 집계 함수인 MAX를 사용했습니다. 집계함수 사용시 행이 없을 때 NULL을 반환하기 때문입니다.
  - MAX나 MIN 무엇이든 사용해도 됩니다.
