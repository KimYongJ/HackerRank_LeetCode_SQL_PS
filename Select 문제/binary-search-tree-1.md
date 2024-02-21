- binary-search-tree-1
  - [https://www.hackerrank.com/challenges/binary-search-tree-1/problem?isFullScreen=true](https://www.hackerrank.com/challenges/binary-search-tree-1/problem?isFullScreen=true)
  ```jsx
  [ 문제 조건 ]
  CREATE TABLE BST (
      N INT,
      P INT
  );
  INSERT INTO BST (N, P) VALUES
  (1, 2),
  (3, 2),
  (6, 8),
  (9, 8),
  (2, 5),
  (8, 5),
  (5, NULL);
  ```
  - **문제 :** BST 테이블은 2개의 컬럼으로 이루어져있습니다. N은 노드번호, P는 부모노드 번호입니다. BST 테이블은 이진트리로 나타낼 수 있습니다. 각 노드가 부모 노드인지, 리프노드인지, 내부 노드인지 출력하는 문제입니다. 노드 번호와 그에 따른 문자열을 한줄로 표현합니다.
  ```jsx
  [ 출력 형식 ]
  1 Leaf
  2 Inner
  3 Leaf
  4 Inner
  5 Leaf
  6 Inner
  7 Leaf
  8 Leaf
  9 Inner
  10 Leaf
  11 Inner
  12 Leaf
  13 Inner
  14 Leaf
  15 Root
  ```
  ```jsx
  [ 정답 ]
  SELECT CONCAT(N, ' ', NODETYPE) AS OUT_PUT
  FROM (
  			SELECT	N
  			,	CASE
  					WHEN P IS NULL THEN 'Root'
  					WHEN (SELECT COUNT(*) FROM BST B WHERE B.P = A.N ) = 0 THEN 'Leaf'
  					ELSE 'Inner'
  				END AS NODETYPE
  			FROM BST A
  	)BST
  ORDER BY N
  ```
  - **해설 :** 이 문제는 각 노드의 특성을 따라 Root, Leaf, Inner 문자열만 잘 생성해주면 됩니다. 해당 문자열은 case when 구문으로 간단히 구할 수 있습니다. 조건은 다음과 같습니다.
    - **Root 노드의 특징은 P값이 NULL인 특징이 있습니다.**
    - **SELECT COUNT(\*) FROM BST B WHERE B.P = A.N ) = 0 :** Leaf 노드는 자식 노드가 없습니다. 이 특징을 활용해 Leaf 노드를 걸러 낼 수 있습니다. 메인 쿼리의 현재 행에 대한 정보를 사용해 자식 노드가 없는 행을 걸러 냅니다. 이런 쿼리를 상호 연관 서브 쿼리라고 합니다. 메인 테이블의 노드 번호가 서브 쿼리의 부모 노드랑 같은 것(한마디로 자식이 있는 노드를 찾는 것)에 대해 count를 합니다. 만약 값이 하나도 없다면 자식 노드가 없다는 뜻이 되어 리프 노드라는 것을 알 수 있습니다.
    - **그 후 Root도 아니고 Leaf도 아닌 것은 Inner로 입력해줍니다.**
  - 위와 같이 구해진 값을 concat 함수로 붙이고, N을 기준으로 오름차순 정렬하면 됩니다.
