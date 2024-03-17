# **Biggest-Single-Number**

- [https://leetcode.com/problems/biggest-single-number/](https://leetcode.com/problems/biggest-single-number/)
- 문제 : MyNumbers 테이블에서 한번만 등장하는 숫자 중 가장 큰 숫자를 고르는 문제이며 숫자가 하나도 없을 때는 null을 출력해야 합니다. 행이 출력이 안되면 안됩니다.

```jsx
[ 문제 조건 ]
CREATE TABLE MyNumbers (
  num INT
);

INSERT INTO MyNumbers (num) VALUES
(8),(8),(3),(3),(1),(1),(4),(4),(5),(5),(6),(6);
```

```jsx
[ 정답 ]
SELECT MAX(NUM) NUM
FROM (
		SELECT NUM
		FROM MYNUMBERS
		GROUP BY NUM
		HAVING COUNT(*) = 1
)MM
```

- **해설 :** 먼저 서브 쿼리에서 num을 기준으로 그룹을 묶은 후 having절에서 1번만 등장하는 숫자를 골라 줍니다. 그 후 외부 쿼리에서 MAX 함수를 사용해 NUM을 출력해줍니다. 이 때 MAX를 사용하면 서브쿼리에 데이터가 없을 때 알아서 NULL을 출력해줍니다.
