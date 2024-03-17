# **Managers-with-at-Least-5-Direct-Reports**

- [https://leetcode.com/problems/managers-with-at-least-5-direct-reports/](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/)
- **문제**
  - "최소 5명의 직접 보고하는 직원을 가진 관리자 찾기"에 관한 SQL 문제입니다. `Employee` 테이블은 직원의 이름, 부서, 그리고 관리자의 ID를 나타냅니다. 목표는 각 관리자 ID에 대해 최소 5명의 직접 보고하는 직원을 가진 관리자의 이름을 찾는 것입니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Employee (
    id INT,
    name VARCHAR(255),
    department VARCHAR(255),
    managerId INT
);
INSERT INTO Employee (id, name, department, managerId) VALUES
(101, 'John', 'A', NULL),(102, 'Dan', 'A', 101),
(103, 'James', 'A', 101),(104, 'Amy', 'A', 101),
(105, 'Anne', 'A', 101),(106, 'Ron', 'B', 101);
```

```jsx
[ 정답 ]
SELECT	NAME
FROM employee
WHERE ID IN(
			SELECT managerId
			FROM EMPLOYEE
			GROUP BY managerId
			HAVING COUNT(*) >=5
)
```

- **해설**
  - 서브쿼리에서 managerId 기준으로 그룹을 지어 5개 이상인 id를 조회합니다. 그 후 메인 테이블의 id값이 해당 managerId와 같을 때 name을 출력해줍니다.
