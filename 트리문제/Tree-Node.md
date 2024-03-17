# **Tree-Node**

- [https://leetcode.com/problems/tree-node/](https://leetcode.com/problems/tree-node/)
- **문제**
  - **`Tree`**라는 이름의 테이블이 있으며, 각 노드는 고유한 **`id`**를 가지고 부모 노드의 **`id`**를 **`p_id`**로 참조합니다.
  - 루트 노드는 **`p_id`**가 **`NULL`**인 노드이며 자식 노드를 가집니다.
  - 내부 노드는 부모 노드와 자식 노드를 모두 가집니다.
  - 잎 노드는 부모 노드는 있지만 자식 노드가 없는 노드입니다.
  - 각 노드의 유형(루트, 내부, 잎)을 식별하여 결과를 반환해야 합니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Tree (
    id INT PRIMARY KEY,
    p_id INT,
    FOREIGN KEY (p_id) REFERENCES Tree(id)
);
INSERT INTO Tree (id, p_id) VALUES
(1, NULL), (2, 1), (3, 1), (4, 2), (5, 2);
```

```jsx
[ 정답(1) ]
SELECT DISTINCT T1.ID
,CASE
		WHEN T1.P_ID IS NULL THEN 'Root'
		WHEN T2.ID IS NOT NULL AND T3.ID IS NOT NULL THEN 'Inner'
		ELSE 'Leaf'
END TYPE
FROM TREE T1
LEFT OUTER JOIN TREE T2 -- 자식노드
	ON T2.P_ID = T1.ID
LEFT OUTER JOIN TREE T3	-- 부모노드
	ON T3.ID = T1.P_ID

[ 정답(2) ]
SELECT T1.ID
,CASE
		WHEN T1.P_ID IS NULL THEN 'Root'
		WHEN (SELECT COUNT(*) FROM TREE T2 WHERE T2.P_ID = T1.ID) = 0 THEN 'Leaf'
		ELSE 'Inner'
END TYPE
FROM TREE T1
```

- **정답(1) 해설**
  - 먼저 메인이 되는 테이블을 하나 잡고, 그 테이블의 자식과 부모 노드 데이터 역할을 할 테이블 2개를 조인합니다. 자식 노드는 T1의 본인ID와, T2의 부모 아이디를 결합합니다. 이 코드의 의미는 메인이되는 테이블의 행을 부모로하는 T2테이블의 데이터를 묶는 것입니다. 즉 T2.ID를 하면 자식 노드가 되는 것입니다.
  - 부모노드 역할을 할 테이블을 조인할 때는 반대로 T1(메인테이블)의 부모 ID가 T3테이블의 ID와 같은 것을 엮습니다. 이렇게 하면 T3.ID를 조회할 때 부모 노드가 되는 것입니다.
  - 이렇게 구해졌다면 CASE WHEN 조건을 걸어 출력만 해주면 됩니다. 이 때 LEFT OUTER JOIN을하여 중복행이 발생될 수 있어 DISTINCT 키워드를 반드시 써주어야 합니다.
- **정답(2) 해설**
  - 위 정답(1)의 코드를 더 개선하여 상관 서브쿼리를 이용해 구현한 코드입니다. Root는 조인을 하지 않아도 구할 수 있습니다. 또한 Leaf노드를 하나 구했다면 나머지는 당연히 Inner 노드이기 때문에 가능한 코드입니다.
  - 리프 노드의 특징은, 나를 부모로하는 ID가 없다는 것입니다. 이 특징을 그대로 상관 서브쿼리에 녹여내어 나(T1 테이블의 ID)를 부모로 하는 아이디(T2.P_ID)의 개수가 0인 것을 찾으면 됩니다.
