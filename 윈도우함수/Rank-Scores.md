# **Rank-Scores**

- [https://leetcode.com/problems/rank-scores/](https://leetcode.com/problems/rank-scores/)
- **문제 :** 주어진 규칙에 따라 순위를 매겨야 합니다
  1. 점수들은 가장 높은 것부터 낮은 순으로 정렬되어야 합니다.
  2. 만약 두 개의 점수가 같다면, 두 점수는 같은 순위를 가져야 합니다.
  3. 동점 이후의 순위는 연속된 정수 값을 가져야 하며, 순위 사이에 빈 공간이 있어서는 안 됩니다.

```jsx
[ 문제 조건 ]
CREATE TABLE Scores (
    id INT,
    score DECIMAL(10, 2)
);
INSERT INTO Scores (id, score) VALUES
(1, 3.50),
(2, 3.65),
(3, 4.00),
(4, 3.85),
(5, 4.00),
(6, 3.65);
```

```jsx
[ 정답 ]
select	score
,		dense_rank() over(order by score desc) 'rank'
from scores;
```

- **해설 :** 윈도우 함수인 dense_rank 함수를 사용합니다.
- **RANK :** `RANK()` 함수는 동일한 값을 가진 행에 같은 순위를 부여한 후, 다음 순위를 결정할 때 "갭"을 두고 순위를 매깁니다. 예를 들어, 만약 두 행이 1등이라면, 다음 순위는 3등이 됩니다 (1, 1, 3, 4, ...). 즉, 동점자 수만큼 순위를 건너뛰게 됩니다.
- **DENSE_RANK :** `DENSE_RANK()` 함수도 동일한 값을 가진 행에 같은 순위를 부여하지만, 다음 순위에는 "갭"을 두지 않고 연속적인 순위를 부여합니다. 예를 들어, 두 행이 1등이면, 다음 순위는 2등이 됩니다 (1, 1, 2, 3, ...). 이 경우 동점자의 수에 관계없이 순위가 1씩 증가합니다.
